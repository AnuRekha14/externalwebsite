<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Chat</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        background-color: #f7f8fa;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
      }
      .chat-container {
        background: #fff;
        border: 1px solid #ddd;
        border-radius: 10px;
        width: 400px;
        padding: 16px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        display: flex;
        flex-direction: column;
      }
      .chat-input-area {
        display: flex;
        border: 1px solid #ccc;
        border-radius: 20px;
        padding: 8px 12px;
        background: #f1f1f1;
      }
      .chat-input {
        flex: 1;
        border: none;
        background: transparent;
        outline: none;
        font-size: 16px;
        padding: 6px;
      }
      .send-button {
        background-color: #0078ff;
        border: none;
        color: white;
        border-radius: 50%;
        width: 36px;
        height: 36px;
        cursor: pointer;
        font-size: 16px;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: background 0.2s;
      }
      .send-button:hover {
        background-color: #005fd1;
      }
      .send-message-button {
        background-color: #00008b;
        color: white;
        padding: 15px 30px;
        font-size: 18px;
        font-weight: bold;
        cursor: pointer;
        border: none;
        display: inline-block;
        text-align: center;
        border-radius: 5px;
        box-shadow: 0 0 0 2px white;
        outline: 2px solid #00008b;
      }
      .send-message-button:hover {
        background-color: #0000a0;
      }
      /* Ensure the embedded chat container fills or scrolls as needed */
      #sfChatInlineContainer {
        flex: 1;
        margin-top: 12px;
        /* You can adjust height / overflow if needed */
        min-height: 300px;
        border: 1px solid #ccc;
      }
    </style>
  </head>
  <body>
    <div class="chat-container">
      <div>
        Please select the menu or enter the message to get started.
      </div>
      <div>
        <br />
        <button class="send-message-button" id="orderButton">
          Need help with my Order
        </button>
        <br /><br />
        <button class="send-message-button" id="caseButton">
          Need help with my Case
        </button>
        <br /><br />
      </div>

      <!-- This div is where Salesforce will render the inline chat UI -->
      <div id="sfChatInlineContainer"></div>

      <div class="chat-input-area">
        <input
          type="text"
          id="chatInput"
          class="chat-input"
          placeholder="Type a message..."
        />
        <button class="send-button" id="sendBtn">➤</button>
      </div>
    </div>

    <!-- Salesforce Embedded Messaging -->
    <script type="text/javascript">
      function initEmbeddedMessaging() {
        try {
          embeddedservice_bootstrap.settings.language = 'en_US';

          // Use inline display mode, point to container div
          embeddedservice_bootstrap.settings.displayMode = 'inline';
          embeddedservice_bootstrap.settings.targetElement = document.getElementById(
            'sfChatInlineContainer'
          );

          embeddedservice_bootstrap.init(
            '00DgK000008l5fZ',
            'Messaging_Channel_for_External_Website',
            'https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540',
            {
              scrt2URL:
                'https://orgfarm-de8616b37d-dev-ed.develop.my.salesforce-scrt.com'
            }
          );
        } catch (err) {
          console.error('Error loading Embedded Messaging: ', err);
        }
      }
    </script>

    <script
      type="text/javascript"
      src="https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js"
      onload="initEmbeddedMessaging()"
    ></script>

    <script>
      function sendTextMessage(msg) {
        if (
          embeddedservice_bootstrap &&
          embeddedservice_bootstrap.utilAPI &&
          embeddedservice_bootstrap.utilAPI.sendTextMessage
        ) {
          embeddedservice_bootstrap.utilAPI.sendTextMessage(msg).catch((e) => {
            console.error('Send message failed', e);
          });
        } else {
          console.warn('Messaging API not available');
        }
      }

      const sendBtn = document.getElementById('sendBtn');
      const chatInput = document.getElementById('chatInput');

      sendBtn.addEventListener('click', () => {
        const message = chatInput.value.trim();
        if (message) {
          chatInput.value = '';
          sendTextMessage(message);
        } else {
          alert('Please enter a message first!');
        }
      });

      chatInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') {
          sendBtn.click();
        }
      });

      const orderButton = document.getElementById('orderButton');
      orderButton.addEventListener('click', function () {
        const orderButtonText = orderButton.textContent.trim();
        sendTextMessage(orderButtonText);
      });

      const caseButton = document.getElementById('caseButton');
      caseButton.addEventListener('click', function () {
        const caseButtonText = caseButton.textContent.trim();
        sendTextMessage(caseButtonText);
      });
    </script>
  </body>
</html>
