<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Agentforce Search Chat Inline</title>

<!-- Explicitly include Embedded Messaging CSS to avoid preload warning -->
<link rel="stylesheet" href="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/styles/embedded-messaging-styling.min.css">

<style>
body { font-family: Arial; text-align: center; margin: 50px; background: #f9f9f9; }
h1 { color: #2c3e50; }
#search-container { margin-top: 30px; }
#search-input { width: 50%; padding: 12px; font-size: 16px; border-radius: 5px; border: 1px solid #ccc; }
#search-button { padding: 12px 20px; font-size: 16px; margin-left: 10px; border-radius: 5px; border: none; background-color: #0070d2; color: white; cursor: pointer; }
#search-button:hover { background-color: #005fb2; }
#chat-container { width: 600px; height: 500px; margin: 30px auto; border: 1px solid #ccc; border-radius: 8px; background: white; display: none; }
</style>
</head>
<body>

<h1>Agentforce Search Chat</h1>
<p>Type a query and click Search to open chat below.</p>

<div id="search-container">
  <input type="text" id="search-input" placeholder="Enter your question...">
  <button id="search-button" disabled>Search</button>
</div>

<!-- Inline chat container -->
<div id="chat-container"></div>

<script type="text/javascript">
function initEmbeddedMessaging() {
    try {
        // Hide default floating chat icon
        embeddedservice_bootstrap.settings.displayHelpButton = false;
        embeddedservice_bootstrap.settings.language = 'en_US';

        embeddedservice_bootstrap.init(
            '00DgK000008l5fZ', // Org ID
            'Messaging_Channel_for_External_Website', // Deployment Name
            'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // Site URL
            {
                scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com',
                widgetLocation: '#chat-container' // Embed chat inline
            }
        );
    } catch (err) {
        console.error('Error initializing Embedded Messaging:', err);
    }
}

// Wait until Embedded Messaging is ready
window.addEventListener("onEmbeddedMessagingReady", () => {
    console.log('Embedded Messaging is ready.');

    // Enable search button
    const searchBtn = document.getElementById('search-button');
    searchBtn.disabled = false;

    // Set hidden pre-chat field
    if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
        embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
            'HiddenPrechatEmail': 'contactreply@mailinator.com'
        });
        console.log('Hidden pre-chat email set.');
    }

    // Show chat container on search button click
    searchBtn.addEventListener('click', () => {
        const query = document.getElementById('search-input').value.trim();
        if (!query) {
            alert('Please enter a search query.');
            return;
        }

        console.log('User search query:', query);

        // Show inline chat
        const chatContainer = document.getElementById('chat-container');
        chatContainer.style.display = 'block';

        // Optionally, you can log or send the search query via hidden pre-chat fields
    });
});
</script>

<script type='text/javascript'
src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js'
onload='initEmbeddedMessaging()'>
</script>

</body>
</html>
