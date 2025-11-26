<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agentforce Search Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
            background: #f9f9f9;
        }

        h1 {
            color: #2c3e50;
        }

        #search-container {
            margin-top: 30px;
        }

        #search-input {
            width: 50%;
            padding: 12px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        #search-button {
            padding: 12px 20px;
            font-size: 16px;
            margin-left: 10px;
            border-radius: 5px;
            border: none;
            background-color: #0070d2;
            color: white;
            cursor: pointer;
        }

        #search-button:hover {
            background-color: #005fb2;
        }
    </style>
</head>
<body>

<h1>Agentforce Search Chat</h1>
<p>Type your question below and click Search to launch the chat.</p>

<div id="search-container">
    <input type="text" id="search-input" placeholder="Enter your query...">
    <button id="search-button">Search</button>
</div>

<script type="text/javascript">
    function initEmbeddedMessaging() {
        try {
            // Hide default floating chat button
            embeddedservice_bootstrap.settings.displayHelpButton = false;

            embeddedservice_bootstrap.settings.language = 'en_US';

            embeddedservice_bootstrap.init(
                '00DgK000008l5fZ', // Org ID
                'Messaging_Channel_for_External_Website', // Deployment Name
                'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540', // Site URL
                {
                    scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
                }
            );
        } catch (err) {
            console.error('Error loading Embedded Messaging: ', err);
        }
    }

    // Set hidden pre-chat email after messaging is ready
    window.addEventListener("onEmbeddedMessagingReady", () => {
        if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
            embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
                'HiddenPrechatEmail': 'contactreply@mailinator.com'
            });
            console.log('Hidden pre-chat email set.');
        }
    });

    // Handle search button click
    document.getElementById('search-button').addEventListener('click', () => {
        const query = document.getElementById('search-input').value.trim();
        if (!query) {
            alert('Please enter a search query.');
            return;
        }

        console.log('User search query:', query);

        if (embeddedservice_bootstrap) {
            // Open chat window
            embeddedservice_bootstrap.bootstrapEmbeddedService();

            // Optionally: send query as a prefilled message
            // Some Salesforce deployments allow sending a message automatically
            // Otherwise, agent will see the pre-chat fields or user can type manually
        } else {
            alert('Chat system is not loaded yet. Please wait a moment.');
        }
    });
</script>

<!-- Salesforce Embedded Messaging bootstrap -->
<script type='text/javascript'
    src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js'
    onload='initEmbeddedMessaging()'>
</script>

</body>
</html>
