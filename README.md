<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Agentforce Search Chat Popup</title>

<!-- Include Embedded Messaging CSS -->
<link rel="stylesheet" href="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/styles/embedded-messaging-styling.min.css">

<style>
body { font-family: Arial; text-align: center; margin: 50px; background: #f9f9f9; }
h1 { color: #2c3e50; }
#search-container { margin-top: 30px; }
#search-input { width: 50%; padding: 12px; font-size: 16px; border-radius: 5px; border: 1px solid #ccc; }
#search-button { padding: 12px 20px; font-size: 16px; margin-left: 10px; border-radius: 5px; border: none; background-color: #0070d2; color: white; cursor: pointer; }
#search-button:hover { background-color: #005fb2; }

/* Chat popup modal */
#chat-popup {
    display: none;
    position: fixed;
    bottom: 50px;
    right: 50px;
    width: 400px;
    height: 500px;
    border: 1px solid #ccc;
    background: white;
    z-index: 1000;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}
#chat-popup #chat-container { width: 100%; height: 100%; }
#close-chat {
    position: absolute;
    top: 5px;
    right: 5px;
    background: #d9534f;
    color: white;
    border: none;
    padding: 4px 8px;
    cursor: pointer;
    border-radius: 4px;
}
#close-chat:hover { background: #c9302c; }
</style>
</head>
<body>

<h1>Agentforce Search Chat</h1>
<p>Type a query and click Search to open chat in a popup.</p>

<div id="search-container">
  <input type="text" id="search-input" placeholder="Enter your question...">
  <button id="search-button" disabled>Search</button>
</div>

<!-- Chat popup modal -->
<div id="chat-popup">
    <button id="close-chat">X</button>
    <div id="chat-container"></div>
</div>

<script type="text/javascript">
function initEmbeddedMessaging() {
    try {
        embeddedservice_bootstrap.settings.displayHelpButton = false;
        embeddedservice_bootstrap.settings.language = 'en_US';

        embeddedservice_bootstrap.init(
            '00DgK000008l5fZ', // Org ID
            'Messaging_Channel_for_External_Website', // Deployment Name
            'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // Site URL
            {
                scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com',
                widgetLocation: '#chat-container' // Embed chat inline in popup
            }
        );
    } catch (err) {
        console.error('Error initializing Embedded Messaging:', err);
    }
}

// When Embedded Messaging is ready
window.addEventListener("onEmbeddedMessagingReady", () => {
    console.log('Embedded Messaging is ready.');

    // Enable search button
    const searchBtn = document.getElementById('search-button');
    searchBtn.disabled = false;

    // Close button logic
    const closeBtn = document.getElementById('close-chat');
    closeBtn.addEventListener('click', () => {
        document.getElementById('chat-popup').style.display = 'none';
    });

    // Search button click: show popup and pass search query
    searchBtn.addEventListener('click', () => {
        const query = document.getElementById('search-input').value.trim();
        if (!query) {
            alert('Please enter a search query.');
            return;
        }

        console.log('User search query:', query);

        // Show chat popup
        document.getElementById('chat-popup').style.display = 'block';

        // Set hidden pre-chat field so agent sees the query
        if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
            embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
                'UserSearchQuery': query
            });
        }
    });
});
</script>

<script type='text/javascript'
src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js'
onload='initEmbeddedMessaging()'>
</script>

</body>
</html>
