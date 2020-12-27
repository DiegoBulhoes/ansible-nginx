# Nginx

Instalação do Nginx para usar como proxy de front-end.

## Sites-enabled

- `nginx_server_name`: Nome do servidor;
- `config_path_nginx`: Local onde estará o arquivo princpal de configuração, default: "/etc/nginx/conf.d/";
- `nginx_root_path`: Localização dos arquivos estatiscos, default: "/usr/share/nginx/html/";
- `nginx_listen_port`: Porta que o Nginx irá atender, default: 80;
- `nginx_add_security`: Habilitar a configuração de seguraça, default: True;
- `nginx_log_domain`: Habilitar a configuração de log por dominio, default: True;
- `nginx_reverse_proxy`: Habilitar a configuração de proxy, default: True; e
- `nginx_subdomains_redirect`: Habilitar a configuração de redirecionamento de subdominio, default: True.

## Variáveis do arquivo: Nginx.conf

- `nginx_user`: Usuário do Nginx, default: "www-data";
- `nginx_worker_processes`: Número de processos de trabalho, default: "auto";
- `nginx_worker_rlimit_nofile`: Número máximo de conexões abertos, default: 65535;
- `nginx_multi_accept`: Se multi_acceptestiver desabilitado, um processo de trabalho aceitará uma nova conexão por vez. Caso contrário, um processo de trabalho aceitará todas as novas conexões de uma vez, default: "on";
- `nginx_worker_connections`: Número máximo de conexões simultâneas que podem ser abertas por um processo de trabalho, default: 65535;

## Variáveis do arquivo: General.conf

- `nginx_enable_robots_txt`: Habilitar o robots.txt: default: True;
- `nginx_bots_log_not_found`: Habilitar logs - robots , default: "off";
- `nginx_bots_access_log`: Habilitar log de acesso de _bots_, default: "off";
- `nginx_enable_gzip`: Habilitar gzip, default: True;
- `nginx_gzip`: , Habilitar a compreensão default: "on";
- `nginx_gzip_vary`: Ativa ou desativa a inserção do campo de cabeçalho de resposta "vary: Accept-Encoding", default: "on";
- `nginx_gzip_proxied`: Ativa ou desativa o gzip de respostas para solicitações em proxy, default: any;
- `nginx_gzip_comp_level`: Define um nível de compactação gzip de uma resposta. Os valores aceitáveis ​​estão na faixa de 1 a 9, default: 5; e
- `nginx_gzip_types`: text/plain text/css application/json - application/javascript.

## Variáveis do arquivo: http.conf

- `nginx_charset`: Especifica o campo de cabeçalho de resposta “Content-Type , default: "utf-8";
- `nginx_sendfile`: Eliminar a etapa de cópia dos dados no buffer e permite a cópia direta dos dados de um descritor de arquivo para outro, default: "on";
- `nginx_tcp_nopush`: Isso permite que o Nginx envie cabeçalhos de resposta HTTP em um pacote logo após o bloco de dados ter sido obtido por **sendfile**, default: "on";
- `nginx_tcp_nodelay`: Diretiva permite a substituição do algoritmo de Nagle , default: "on";
- `nginx_server_tokens`: Habilita ou desabilita a emissão da versão Nginx nas páginas de erro e no campo de cabeçalho de resposta “Servidor”, default: "off";
- `nginx_types_hash_max_size`: Define o tamanho máximo da tabela hash, default: "2048"; e
- `nginx_client_max_body_size`: Define o tamanho máximo permitido do corpo da solicitação do cliente, default: "16M".

## Variáveis do arquivo: Proxy.conf

- `nginx_proxy_connect_timeout`: Define um tempo limite para estabelecer uma conexão com um servidor proxy, default: "60s";
- `nginx_proxy_send_timeout`: Define um tempo limite para transmitir uma solicitação ao servidor proxy , default: "60s"; e
- `nginx_proxy_read_timeout`: Define um tempo limite para ler uma resposta do servidor proxy, default: "60s".

## Backend servers:

- `nginx_proxy_backends_custom`: Lista de dicionários de servidores back-end com os seguintes campos:

  - `proxy_redirect`: Define o texto que deve ser alterado nos campos de cabeçalho "Location" e "Refresh" de uma resposta do servidor proxy;
  - `proxy_buffering`: Habilita ou desabilita o buffer de respostas do servidor proxy;
  - `proxy_http_version`: Define a versão do protocolo HTTP para proxy;
  - `proxy_cache_bypass`: Define as condições sob as quais a resposta não será obtida de um cache;
  - `proxy_set_header`: Permite redefinir ou anexar campos ao cabeçalho da solicitação passada ao servidor proxy, por exemplo:

    - Upgrade
    - Connection
    - Host
    - X-Real-IP
    - X-Forwarded-For
    - X-Forwarded-Proto
    - X-Forwarded-Host
    - X-Forwarded-Port
    - Proxy-Connection

  - `proxy_connect_timeout`: Tempo limite para estabelecer uma conexão com um servidor proxy;
  - `proxy_send_timeout`: Tempo limite para transmitir uma solicitação ao servidor proxy;
  - `proxy_read_timeout`: Tempo limite para ler uma resposta do servidor proxy;

- `nginx_proxy_backends_simple`: Lista de dicionários de servidores back-end com os seguintes campos, nos quais estara configurado o proxy com os seguintes valores:

```text
proxy_http_version                 1.1;
proxy_cache_bypass                 $http_upgrade;

# Proxy headers
proxy_set_header Upgrade           $http_upgrade;
proxy_set_header Connection        "upgrade";
proxy_set_header Host              $host;
proxy_set_header X-Real-IP         $remote_addr;
proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-Host  $host;
proxy_set_header X-Forwarded-Port  $server_port;

# Proxy timeouts
proxy_connect_timeout              {{nginx_proxy_connect_timeout}};
proxy_send_timeout                 {{nginx_proxy_send_timeout}};
proxy_read_timeout                 {{nginx_proxy_read_timeout}};
```

Os valores das seguintes diretivas poderão ser alteradas, com essa seguintes variáveis: `nginx_proxy_connect_timeout`, `nginx_proxy_send_timeout` e `nginx_proxy_read_timeout`

```text
proxy_connect_timeout
proxy_send_timeout
proxy_read_timeout
```
