<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Agentforce Demo</title>
</head>
<body>
  <h1>Agentforce Demo</h1>

  <!-- Embedded Messaging Snippet -->
  <script type='text/javascript'>
    function initEmbeddedMessaging() {
      try {
        embeddedservice_bootstrap.settings.language = 'en_US'; // Language

        embeddedservice_bootstrap.init(
          '00DgK000008l5fZ',  // Org ID
          'Messaging_Channel_for_External_Website', // Deployment name
          'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540',
          {
            scrt2URL: 'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
          }
        );
      } catch (err) {
        console.error('Error loading Embedded Messaging: ', err);
      }
    };
  </script>
  <script type='text/javascript' 
          src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js' 
          onload='initEmbeddedMessaging()'></script>

  <!-- Optional: message explaining -->
  <p>Click the button to start a chat with Agentforce.</p>

</body>
</html>
