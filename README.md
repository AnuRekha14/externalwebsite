<html lang="en">
    <head>
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
        </style>

        <!-- Embedded Chat Init Script -->
        <script type='text/javascript'>
            function initEmbeddedMessaging() {
                try {
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
            };
        </script>

        <script 
            type='text/javascript'
            src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js'
            onload='initEmbeddedMessaging()'>
        </script>
    </head>
    
    <body>
        <div>
            Welcome to our Chat Service!
            <br/><br/>
        </div>
        <div class="chat-container">
            <div>
                Please select the menu or enter the message to get started.
                <br/>
            </div>
            <div>
                <br/><br/>
                <button class="send-message-button" id="orderButton">
                    Need help with my Order
                </button>
                <br/><br/>
                <button class="send-message-button" id="caseButton">
                    Need help with my Case
                </button>
                <br/><br/>
            </div>
            <div class="chat-input-area">
                <input type="text" id="chatInput" class="chat-input" placeholder="Type a message..." />
                <button class="send-button" id="sendBtn">➤</button>
            </div>
        </div>

        <script>
            function showChatContainer() {
                const chatContainer = document.querySelector('.chat-container');
                chatContainer.style.display = 'block';
            }

            function hideChatContainer() {
                const chatContainer = document.querySelector('.chat-container');
                chatContainer.style.display = 'none';
            }
            
            function launchChat(message) {
                embeddedservice_bootstrap.utilAPI.launchChat()
                    .then(() => {
                        console.log('Successfully launched Messaging');
                        sendMessageToChat(message);
                    })
                    .catch(() => {
                        console.log('Some error occurred when launching Messaging');
                    })
                    .finally(() => {
                        console.log('Successfully launched Messaging - Finally');
                    });
            }
            
            function sendMessageToChat(message) {
                setTimeout(() => {
                    embeddedservice_bootstrap.utilAPI.sendTextMessage(message)
                        .then(() => {
                            console.log("Message sent");
                        })
                        .catch(() => {
                            console.log("Message not sent");
                        })
                        .finally(() => {
                            console.log("Message sent - finally");
                        });
                }, 8000);
            }
            
            const sendBtn = document.getElementById('sendBtn');
            const chatInput = document.getElementById('chatInput');
            sendBtn.addEventListener('click', () => {
                const message = chatInput.value.trim();
                if (message) {
                    console.log(message);
                    chatInput.value = '';
                    hideChatContainer();
                    launchChat(message);
                } else {
                    alert("Please enter a message first!");
                }
            });

            chatInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    sendBtn.click();
                }
            });
            
            const orderButton = document.getElementById('orderButton');
            orderButton.addEventListener('click', function() {
                const orderButtonText = orderButton.textContent.trim();
                console.log(orderButtonText);
                hideChatContainer(); // Close popup immediately
                launchChat(orderButtonText);
            });
            
            const caseButton = document.getElementById('caseButton');
            caseButton.addEventListener('click', function() {
                const caseButtonText = caseButton.textContent.trim();
                console.log(caseButtonText);
                hideChatContainer(); // Close popup immediately
                launchChat(caseButtonText);
            }); 
        </script>
    </body>
</html>
