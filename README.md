# eureka-cc-mirror
https://eureka-cc-mirror.bddjr.cn

***
nginx proxy config
```
location ^~ / {
    proxy_pass https://eureka.codingclip.cc; 
    proxy_set_header Host eureka.codingclip.cc; 
    proxy_set_header X-Real-IP $remote_addr; 
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    proxy_set_header REMOTE-HOST $remote_addr; 
    proxy_set_header Upgrade $http_upgrade; 
    proxy_set_header Connection "upgrade"; 
    proxy_set_header X-Forwarded-Proto $scheme; 
    proxy_http_version 1.1; 
    add_header X-Cache $upstream_cache_status; 
    if ( $uri ~* "\.(gif|png|jpg|css|js|woff|woff2)$" ) {
        expires 1m; 
    }
    proxy_ignore_headers Set-Cookie Cache-Control expires; 
    proxy_cache proxy_cache_panel; 
    proxy_cache_key $host$uri$is_args$args; 
    proxy_cache_valid 200 304 301 302 10m; 
    proxy_ssl_server_name on;
    proxy_cache_revalidate on;
    proxy_next_upstream error timeout http_502 http_500 http_429 non_idempotent invalid_header ;
    proxy_next_upstream_tries 3;
    proxy_request_buffering on;
    client_body_buffer_size 10M;
    client_body_in_file_only off;
    client_body_timeout 30s;
}
```
