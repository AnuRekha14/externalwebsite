<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Agentforce</title>
  <meta name="description" content="Minimal Google-style search demo page" />
  <style>
    :root{ --bg:#ffffff; --muted:#70757a; --accent:#1a73e8; }
    html,body{height:100%;}
    body{
      margin:0; background:var(--bg); font-family: Arial, Helvetica, sans-serif;
      color:#202124; -webkit-font-smoothing:antialiased; display:flex; align-items:center;
      justify-content:center; min-height:100vh; padding:24px; box-sizing:border-box;
    }

    .container{ text-align:center; width:100%; max-width:760px; }
    .logo{ font-size:64px; font-weight:400; margin:0; letter-spacing:-1px; }
    .logo .accent{ color:var(--accent); font-weight:700; }
    .sub{ color:var(--muted); margin-top:6px; font-size:14px; }

    .search-wrap{ margin-top:28px; display:flex; justify-content:center; }
    .search{ width:100%; max-width:640px; display:flex; align-items:center; border:1px solid #dfe1e5;
            padding:14px 16px; border-radius:24px; box-shadow:0 1px 3px rgba(60,64,67,0.08); }
    .search:focus-within{ box-shadow:0 4px 12px rgba(26,115,232,0.12); border-color:rgba(26,115,232,0.6); }
    .search-input{ border:0; outline:none; font-size:18px; flex:1; }
    .search-btn{ margin-left:12px; padding:10px 14px; border-radius:6px; border:1px solid #dadce0; background:#f8f9fa; cursor:pointer; }

    .links{ margin-top:18px; color:var(--muted); font-size:13px; }
    footer{ position:fixed; bottom:12px; left:0; right:0; text-align:center; color:var(--muted); font-size:12px; }

    @media (max-width:640px){ .logo{ font-size:48px; } .search{ padding:12px; } }
  </style>
</head>
<body>
  <div class="container" role="main">
    <h1 class="logo"><span class="accent">Agent</span>force</h1>
    <div class="sub">A simple search-style demo page</div>

    <div class="search-wrap" aria-label="Search">
      <div class="search" role="search">
        <input id="q" class="search-input" type="search" placeholder="Search or ask a question" aria-label="Search" />
        <button id="go" class="search-btn" aria-label="Search">Search</button>
      </div>
    </div>

    <div class="links" aria-hidden="true">This is a demo layout for a client presentation.</div>
  </div>

  <!--
    OPTIONAL: If you want to integrate a chat/assistant here, paste the Salesforce "Embedded Service" / "Messaging" snippet
    between the <script> tags below. The page intentionally does not mention or display the integration — it simply
    provides a Google-style front-end for demos.

    Replace the comment in the script tag below with the snippet from Salesforce Setup → Embedded Service Deployments → Get Code
  -->
<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

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
<script type='text/javascript' src='https://orgfarm-de8616b37d-dev-ed.develop.my.site.com/ESWMessagingChannelfor1759308457540/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>


  <script>
    // Small demo behaviour: hitting Enter or clicking Search opens a new tab with a simple search query (for demo only).
    (function(){
      const q = document.getElementById('q');
      const btn = document.getElementById('go');
      function doSearch(){
        const v = (q.value || '').trim();
        // For client demo we just perform a harmless search -- change to any behavior you like.
        if (!v) return;
        // Open a new tab showing a search results page (Google-style behavior for demo). No analytics, no tracking.
        const url = 'https://www.google.com/search?q=' + encodeURIComponent(v);
        window.open(url, '_blank');
      }
      btn.addEventListener('click', doSearch);
      q.addEventListener('keydown', function(ev){ if (ev.key === 'Enter') { ev.preventDefault(); doSearch(); } });
    })();
  </script>

  <footer>Demo — built for presentation</footer>
</body>
</html>
