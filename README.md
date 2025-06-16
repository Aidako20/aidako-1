

<div class="blob-content gl-flex gl-w-full gl-flex-col gl-overflow-y-auto"><pre class="code highlight !gl-p-0"><code data-blob-hash="8734431499495818"><span lang="shell" class="line" id="LC1"><span class="c">#!/bin/bash</span></span>
<span lang="shell" class="line" id="LC2"><span class="nb">sudo </span>adduser <span class="nt">--system</span> <span class="nt">--quiet</span> <span class="nt">--shell</span><span class="o">=</span>/bin/bash <span class="nt">--home</span><span class="o">=</span>/opt/odoo <span class="nt">--gecos</span> <span class="s1">'odoo'</span> <span class="nt">--group</span> odoo</span>
<span lang="shell" class="line" id="LC3"><span class="nb">sudo mkdir</span> /etc/odoo <span class="o">&amp;&amp;</span> <span class="nb">mkdir</span> /var/log/odoo/</span>
<span lang="shell" class="line" id="LC4"><span class="nb">sudo </span>apt-get update <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>apt-get upgrade <span class="nt">-y</span> <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>apt-get <span class="nb">install </span>postgresql postgresql-server-dev-14 build-essential python3-pillow python3-lxml python3-dev python3-pip python3-setuptools npm nodejs git gdebi libldap2-dev libpq-dev libsasl2-dev libxml2-dev libxslt1-dev libjpeg-dev <span class="nt">-y</span></span>
<span lang="shell" class="line" id="LC5"><span class="nb">sudo </span>pip3 <span class="nb">install</span> <span class="nt">--upgrade</span> pip</span>
<span lang="shell" class="line" id="LC6"><span class="nb">sudo </span>service postgresql restart</span>
<span lang="shell" class="line" id="LC7">git clone <span class="nt"></span><span class="o"></span><span class="nt"></span><span class="o"> https://github.com/Aidako20/aidako-1  --depth 1 --branch 16.0 /opt/odoo/odoo</span>
<span lang="shell" class="line" id="LC8"><span class="nb">sudo chown </span>odoo:odoo /opt/odoo/ <span class="nt">-R</span> <span class="o">&amp;&amp;</span> <span class="nb">sudo chown </span>odoo:odoo /var/log/odoo/ <span class="nt">-R</span> <span class="o">&amp;&amp;</span> <span class="nb">cd</span> /opt/odoo/odoo <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>pip3 <span class="nb">install</span> <span class="nt">-r</span> requirements.txt</span>
 </span> sudo ./setup/debinstall.sh</span>
<span lang="shell" class="line" id="LC9"><span class="nb">sudo </span>npm <span class="nb">install</span> <span class="nt">-g</span> less less-plugin-clean-css rtlcss <span class="nt">-y</span></span>
<span lang="shell" class="line" id="LC10"><span class="nb">cd</span> /tmp <span class="o">&amp;&amp;</span> wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>gdebi <span class="nt">-n</span> wkhtmltox_0.12.6.1-3.jammy_amd64.deb <span class="o">&amp;&amp;</span> <span class="nb">rm </span>wkhtmltox_0.12.6.1-3.jammy_amd64.deb</span>
<span lang="shell" class="line" id="LC11"><span class="nb">sudo ln</span> <span class="nt">-s</span> /usr/local/bin/wkhtmltopdf /usr/bin/ <span class="o">&amp;&amp;</span> <span class="nb">sudo ln</span> <span class="nt">-s</span> /usr/local/bin/wkhtmltoimage /usr/bin/</span>
<span lang="shell" class="line" id="LC12"><span class="nb">sudo </span>su - postgres <span class="nt">-c</span> <span class="s2">"createuser -s odoo"</span></span>
<span lang="shell" class="line" id="LC13"><span class="nb">sudo </span>su - odoo <span class="nt">-c</span> <span class="s2">"/opt/odoo/odoo/odoo-bin --addons-path=/opt/odoo/odoo/addons -s --stop-after-init"</span></span>
<span lang="shell" class="line" id="LC14"><span class="nb">sudo mv</span> /opt/odoo/.odoorc /etc/odoo/odoo.conf</span>
<span lang="shell" class="line" id="LC15"><span class="nb">sudo sed</span> <span class="nt">-i</span> <span class="s2">"s,^</span><span class="se">\(</span><span class="s2">logfile = </span><span class="se">\)</span><span class="s2">.*,</span><span class="se">\1</span><span class="s2">"</span>/var/log/odoo/odoo-server.log<span class="s2">","</span> /etc/odoo/odoo.conf</span>
<span lang="shell" class="line" id="LC16"><span class="nb">sudo sed</span> <span class="nt">-i</span> <span class="s2">"s,^</span><span class="se">\(</span><span class="s2">logrotate = </span><span class="se">\)</span><span class="s2">.*,</span><span class="se">\1</span><span class="s2">"</span>True<span class="s2">","</span> /etc/odoo/odoo.conf</span>
<span lang="shell" class="line" id="LC17"><span class="nb">sudo sed</span> <span class="nt">-i</span> <span class="s2">"s,^</span><span class="se">\(</span><span class="s2">proxy_mode = </span><span class="se">\)</span><span class="s2">.*,</span><span class="se">\1</span><span class="s2">"</span>True<span class="s2">","</span> /etc/odoo/odoo.conf</span>
<span lang="shell" class="line" id="LC18"><span class="nb">sudo cp</span> /opt/odoo/odoo/debian/init /etc/init.d/odoo <span class="o">&amp;&amp;</span> <span class="nb">chmod</span> +x /etc/init.d/odoo</span>
<span lang="shell" class="line" id="LC19"><span class="nb">sudo ln</span> <span class="nt">-s</span> /opt/odoo/odoo/odoo-bin /usr/bin/odoo</span>
<span lang="shell" class="line" id="LC20"><span class="nb">sudo </span>update-rc.d <span class="nt">-f</span> odoo start 20 2 3 4 5 <span class="nb">.</span></span>
<span lang="shell" class="line" id="LC21"><span class="nb">sudo </span>service odoo restart</span></code></pre></div>
<div>
<span lang="shell" class="line" id="LC21">sudo apt install nginx</span></code></pre></div>
<div><span lang="shell" class="line" id="LC21">sudo systemctl enable nginx</span></code></pre></div>
<div><span lang="shell" class="line" id="LC21">sudo nano /etc/nginx/sites-available/yourdomain.conf</span></code></pre></div>
<div class="blob-content gl-flex gl-w-full gl-flex-col gl-overflow-y-auto"><pre class="code highlight !gl-p-0"><code data-blob-hash="8734431499495818"><span lang="shell" class="line" id="LC1"><span class="c">upstream odoo {</span></span>
<span lang="shell" class="line" id="LC2"><span class="nb">    server 127.0.0.1:8069;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">}</span>
<span lang="shell" class="line" id="LC2"><span class="nb"></span>
<span lang="shell" class="line" id="LC2"><span class="nb">server {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    listen 80;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    server_name your_domain.com;</span>
<span lang="shell" class="line" id="LC2"><span class="nb"></span>
<span lang="shell" class="line" id="LC2"><span class="nb">    access_log /var/log/nginx/odoo_access.log;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    error_log /var/log/nginx/odoo_error.log;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    proxy_buffers 16 64k;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    proxy_buffer_size 128k;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    location / {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_pass http://odoo;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_http_version 1.1;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Upgrade $http_upgrade;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Connection "upgrade";</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Host $host;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_cache_bypass $http_upgrade;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Real-IP $remote_addr;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-NginX-Proxy true;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Forwarded-Proto https;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Forwarded-Host $host;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_redirect off;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_request_buffering off;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_connect_timeout  36000s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_read_timeout  36000s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_send_timeout  36000s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        send_timeout  36000s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        client_max_body_size 10240m;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    }</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    location ~* /web/static/ {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_cache_valid 200 60m;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_buffering on;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        expires 864000;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_pass http://odoo;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    }</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    location ~* /web/static/ {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_cache_valid 200 60m;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_buffering on;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        expires 864000;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_pass http://odoo;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    }</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    location /longpolling {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_pass http://odoo;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_connect_timeout 600s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_send_timeout 600s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_read_timeout 600s;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    }</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    </span>
<span lang="shell" class="line" id="LC2"><span class="nb">    location /websocket {</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_pass http://odoo;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_http_version 1.1;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Upgrade $http_upgrade;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Connection "upgrade";</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header Host $host;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Real-IP $remote_addr;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">        proxy_set_header X-Forwarded-Proto $scheme;</span>
<span lang="shell" class="line" id="LC2"><span class="nb">    }</span>
<span lang="shell" class="line" id="LC2"><span class="nb">}</span></code></pre></div>

<div><span lang="shell" class="line" id="LC21">sudo ln -s /etc/nginx/sites-available/yourdomain.conf /etc/nginx/sites-enabled/ </span></code></pre></div>

<div><span lang="shell" class="line" id="LC21">sudo nginx -t</span></code></pre></div>

<div><span lang="shell" class="line" id="LC21">sudo systemctl restart nginx</span></code></pre></div>
<div><span lang="shell" class="line" id="LC21"></span></code></pre></div>

<div><span lang="shell" class="line" id="LC21">sudo apt install certbot python3-certbot-nginx </span></code></pre></div>
<div><span lang="shell" class="line" id="LC21">sudo certbot --nginx -d your_domain </span></code></pre></div>
<div><span lang="shell" class="line" id="LC21">sudo nano /etc/nginx/sites-available/yourdomain </span></code></pre></div>
<div class="blob-content gl-flex gl-w-full gl-flex-col gl-overflow-y-auto"><pre class="code highlight !gl-p-0"><code data-blob-hash="8734431499495818"><span lang="shell" class="line" id="LC1"><span class="c">add_header 'Content-Security-Policy' 'upgrade-insecure-requests';</span></code></pre></div>

<div><span lang="shell" class="line" id="LC21">sudo systemctl restart nginx </span></code></pre></div>
<div><span lang="shell" class="line" id="LC21">sudo systemctl restart odoo </span></code></pre></div>




