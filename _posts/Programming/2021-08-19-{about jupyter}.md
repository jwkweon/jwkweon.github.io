---
layout: single
title: '[Jupyter Notebook]실행은 했는데 웹 브라우저에서 열리지 않을 때'
categories:
  - Programming
tags:
  - Jupyter Notebook
  - Jupyter Notebook Error
comments: true  
use_math: true
classes: wide
toc: false
date:   2021-08-19 00:00:00 
lastmod : 2021-08-19 23:59:59 
sitemap :
  changefreq : daily
  priority : 1.0
---
## [Jupyter Notebook]실행은 했는데 웹 브라우저에서 열리지 않을 때

어느날 ubuntu 서버에 접속해 원격으로 코딩을 하던중 문제가 발생하였다. 서버 컴퓨터를 재부팅한 뒤 jupyter notebook 명령어 `jupyter notebook --ip xxx.xxx.xxx.xxx --no-browser` 를 입력한 뒤 터미널 창에서는 동작을 하였지만 웹 브라우저(Chrome을 사용)에서 '응답하는 데 시간이 너무 오래 걸립니다.'라는 문구와 함께 노트북 창이 열리지 않았다.  


### jupyter system 전체 삭제  
문제를 해결하기 위해 첫 번째 방법으로 jupyter notebook을 삭제한 후 재설치 해주었다.  

`python3 -m pip uninstall -y jupyter jupyter_core jupyter-client jupyter-console jupyterlab_pygments notebook qtconsole nbconvert nbformat`  

### jupyter 설치
`pip3 install notebook`  

하지만 문제는 해결되지 않았고 여전히 웹 브라우저에서의 응답은 없었다.  
다음으로 notebook 실행 명령어에서 port를 8888이 아닌 8022와 같은 다른 port로 변경해보았지만 여전히 동작하지 않았다. (`jupyter notebook --ip xxx.xxx.xxx.xxx --port=8022 --allow-root` 등 명령어 실행)  

터미널에서 실행은 되지만 웹브라우저에서 거절이 되었기에 8888 port에 대한 접근이 기본 ubuntu 방화벽에서 허용되지 않은것 같다고 생각이 들었고 다음 명령어를 통해 port를 허용해 주었다.  

방화벽에서 port 허용  
```terminal
$ sudo ufw allow 8888
Rule added
Rule added (v6)
```  
방화벽 reload  
```terminal
$ sudo ufw reload
Firewall reloaded
```  
이후 jupyter notebook은 웹 브라우저에서 잘 동작함을 확인하였다. 모종의 이유로 방화벽에서 몇개의 port들에 대한 접근이 막혔던 것 같다. 