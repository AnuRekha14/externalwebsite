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
<p>Type your question and click Search to launch the chat.</p>

<div id="search-container">
  <input type="text" id="search-input" placeholder="Enter your query...">
  <button id="search-button" disabled>Search</button>
</div>

<script type="text/javascript">
  function initEmbeddedMessaging() {
    try {
      // Hide the default chat button before init
      embeddedservice_bootstrap.settings.displayHelpButton = false;

      embeddedservice_bootstrap.settings.language = 'en_US';

      embeddedservice_bootstrap.init(
        '00DgK000008l5fZ',
        'Messaging_Channel_for_External_Website',
        'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540',
        {
          scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
        }
      );
    } catch (err) {
      console.error('Error loading Embedded Messaging: ', err);
    }
  }

  // Wait until embedded messaging is ready
  window.addEventListener("onEmbeddedMessagingReady", () => {
    console.log('Embedded Messaging ready');

    // Enable the search button only after EM is ready
    const searchButton = document.getElementById('search-button');
    searchButton.disabled = false;

    // Set hidden pre-chat field
    if (embeddedservice_bootstrap && embeddedservice_bootstrap.prechatAPI) {
      embeddedservice_bootstrap.prechatAPI.setHiddenPrechatFields({
        'HiddenPrechatEmail': 'contactreply@mailinator.com'
      });
      console.log('Hidden pre-chat email set.');
    }

    // Attach click handler
    searchButton.addEventListener('click', () => {
      const query = document.getElementById('search-input').value.trim();
      if (!query) {
        alert('Please enter a search query.');
        return;
      }

      console.log('User search query:', query);

      // Launch the chat
      if (embeddedservice_bootstrap) {
        embeddedservice_bootstrap.bootstrapEmbeddedService();
        // Optionally, you can log the search query or send to agent via custom logic
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
