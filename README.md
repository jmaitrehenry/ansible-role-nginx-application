# Ansible role for creating nginx application

Ansible role for creating server block for [nginx](http://http://nginx.org//)

[![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org)

## Installation
```
$ ansible-galaxy install jmaitrehenry.nginx-application
```

## Getting started
```
---
- hosts: grafana.example.com
  roles:
    - jmaitrehenry.nginx # or a valid nginx installation
    - jmaitrehenry.nginx-application
```

## Configurables
```
---
nginx_applications:
  -
    name: "default"
    port: "80 default"
    path: "/var/www"
    gzip: true
    options:
      - { key: "underscores_in_headers", value: "on"}
    locations:
      -
        path: "/"
        proxy: false
        try_files: "$uri /index.html"
        options:
          - { key: "add_header", value: "X-Robots-Tag noindex"}
      -
        path: "/api"
        proxy: true
        proxy_pass: "https://api.example.com"
        proxy_http_version: "1.1"
  -
    name: "www.example.com"
    port: 80
    options:
      - { key: "return", value: "301 https://example.com$request_uri" }
  -
    name: "deleted.com"
    deleted: true
```

## Contributing
Contributions, questions, and comments are all welcomed and encouraged!

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## Credits

- [Julien Maitrehenry](https://github.com/jmaitrehenry)

## License

The MIT License

Copyright (c) 2015 PetalMD https://www.petalmd.com

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
