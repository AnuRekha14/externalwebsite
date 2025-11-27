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
                            scrt2URL: 'https://orgfarm-de8616b37d-dev-
