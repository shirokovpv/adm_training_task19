# adm_training_task19
<h1 align="center">Занятие 19. Разворачиваем сетевую лабораторию</h1>
<ol>
<li><span style="font-weight: 400;">Развернуть Vagrant-стенд&nbsp;</span></li>
<li><span style="font-weight: 400;"> Построить следующую сетевую архитектуру:</span></li>
</ol>
<p><span style="font-weight: 400;">Сеть office1</span></p>
<p><span style="font-weight: 400;">- 192.168.2.0/26&nbsp; &nbsp; &nbsp; - dev</span></p>
<p><span style="font-weight: 400;">- 192.168.2.64/26 &nbsp; &nbsp; - test servers</span></p>
<p><span style="font-weight: 400;">- 192.168.2.128/26&nbsp; &nbsp; - managers</span></p>
<p><span style="font-weight: 400;">- 192.168.2.192/26&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">Сеть office2</span></p>
<p><span style="font-weight: 400;">- 192.168.1.0/25&nbsp; &nbsp; &nbsp; - dev</span></p>
<p><span style="font-weight: 400;">- 192.168.1.128/26&nbsp; &nbsp; - test servers</span></p>
<p><span style="font-weight: 400;">- 192.168.1.192/26&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">Сеть central</span></p>
<p><span style="font-weight: 400;">- 192.168.0.0/28 &nbsp; &nbsp; - directors</span></p>
<p><span style="font-weight: 400;">- 192.168.0.32/28&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">- 192.168.0.64/26&nbsp; &nbsp; - wifi</span></p>
<p><span style="font-weight: 400;">Итого должны получиться следующие сервера:</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">inetRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">centralRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office1Router</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office2Router</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">centralServer</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office1Server</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office2Server</span></li>
</ul>
<p><span style="font-weight: 400;">В практической части требуется:&nbsp;</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">Соединить офисы в сеть согласно логической схеме и настроить роутинг</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Интернет-трафик со всех серверов должен ходить через inetRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Все сервера должны видеть друг друга (должен проходить ping)</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Добавить дополнительные сетевые интерфейсы, если потребуется</span></li>
</ul>
<h3 class="western"><a name="_heading=h.df570rpzx1qg"></a><span style="font-family: Roboto, serif;"><span style="font-size: small;">Используемые ОС</span></span></h3>
<p style="line-height: 108%; margin-bottom: 0.28cm;" align="justify"><span style="font-family: Roboto, serif;">Хостовая ОС Ubuntu 24.04 Desktop с установленным Vagrant 2.3.5. VirtualBox версия 7.0.16_Ubuntu r162802</span></span></p>
<h3 class="western"><span style="font-family: Roboto, serif;"><span style="font-size: small;">Выполнение</span></span></h3>
<p>******************************</p>
<p>Ввиду невозможности в нынешних реалиях воспользоваться стандартными репозиториями Vagrant (в РФ они сейчас не доступны), предложено обходное решение. Использован репозиторий, развернутый на&nbsp;<a href="https://vagrant.elab.pro/" rel="nofollow">https://vagrant.elab.pro/</a></p>
<p>Так как официальный пакет последней версии Vagrant также не доступен для скачивания, пакет взят оттуда же. Версия 2.3.5.</p>
<img width="411" height="88" alt="image" src="https://github.com/user-attachments/assets/7591c684-f543-4bf6-bfa8-3706a7648c97" />
<p>&nbsp;</p>
<p>Для подключения репозитория надо добавить в Vagrant-файл строку:</p>
<p><code>ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'</code></p>
<p>И изменить box_name и box_version (как в репозитории, если туда зайти).</p>
<img width="272" height="153" alt="image" src="https://github.com/user-attachments/assets/8a216a0c-b904-48e5-aa78-bd21d80e3052" />
<p>******************************</p>
<p>Создаем каталог ~/task19, а в нем Vagrantfile для развертывания виртуальных машин. Скачаем Vagrantfile из репозитория https://github.com/erlong15/otus-linux/tree/network
и изменим его в соответствии с заданием и обходным решением, описанным выше. ОС Ubuntu 22.04, добавляем новые ВМ и сетевые настройки для них. Измененный файл прикладываю сюда.</p>
<p>После выполнения команды <code>vagrant up</code> получим 7 виртуальных машин.</p>
<img width="1089" height="562" alt="image" src="https://github.com/user-attachments/assets/6dfede39-7dc0-4f82-a807-149d5c8b3b4b" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">После того, как все 7 серверов у нас развернуты, нам нужно настроить маршрутизацию и NAT таким образом, чтобы доступ в Интернет со всех хостов был через inetRouter и каждый сервер должен быть доступен с любого из 7 хостов.</span></p>
<img width="693" height="841" alt="image" src="https://github.com/user-attachments/assets/8a5542ff-b864-419d-9274-9576d0a391c5" />
<p><strong>Настройка NAT</strong></p>
<p><span style="font-weight: 400;">1) Подключимся по SSH к ВМ inetRouter:</p>
<p><span style="font-weight: 400;"><code>vagrant ssh inetRouter</code></p>
<p><span style="font-weight: 400;"><code>sudo -i</code></p>
<p><span style="font-weight: 400;">2) Проверим, включен ли файервол: <code>systemctl status ufw</code></p>
<img width="715" height="210" alt="image" src="https://github.com/user-attachments/assets/529f8473-6179-4148-b828-2c86d2939370" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">Останавливаем и отключаем:</span></p>
<p><code>systemctl stop ufw</code></p>
<p><code>systemctl disable ufw</code></p>
<img width="812" height="118" alt="image" src="https://github.com/user-attachments/assets/e022d068-ff5e-4f07-8220-040116873009" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">3) Создаём файл <strong>/etc/iptables_rules.ipv4</strong></p>
<p><code>nano /etc/iptables_rules.ipv4</code></p>
<p>*filter<br />:INPUT ACCEPT [90:8713]<br />:FORWARD ACCEPT [0:0]<br />:OUTPUT ACCEPT [54:7429]<br />-A INPUT -p icmp -j ACCEPT<br />-A INPUT -i lo -j ACCEPT<br />-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT<br />COMMIT</p>
<p>*nat<br />:PREROUTING ACCEPT [1:44]<br />:INPUT ACCEPT [1:44]<br />:OUTPUT ACCEPT [0:0]<br />:POSTROUTING ACCEPT [0:0]<br />-A POSTROUTING ! -d 192.168.0.0/16 -o eth0 -j MASQUERADE<br />COMMIT</p>
<img width="540" height="331" alt="image" src="https://github.com/user-attachments/assets/fa1903d2-ff0e-4c2d-832a-372833ac5ae1" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">4) Создаём файл, в который добавим скрипт автоматического восстановления правил при перезапуске системы:</span></p>
<p><code>nano /etc/network/if-pre-up.d/iptables</code></p>
<p><span style="font-weight: 400;">#!/bin/sh</span></p>
<p><span style="font-weight: 400;">/sbin/iptables-restore &lt; /etc/iptables_rules.ipv4</span></p>
<img width="540" height="79" alt="image" src="https://github.com/user-attachments/assets/c2ae199a-84a3-4218-8a06-7146297faf19" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">5) Добавляем права на выполнение файла /etc/network/if-pre-up.d/iptables</span></p>
<p><code>chmod +x /etc/network/if-pre-up.d/iptables</code></p>
<p><span style="font-weight: 400;">6) Перезагружаем сервер: <code>reboot</code></p>
<p><span style="font-weight: 400;">7) После перезагрузки сервера проверяем правила iptables: <code>iptables-save</code></p>
<p><strong>Настройка NAT через Ansible</strong></p>
<p><span style="font-weight: 400;">Выполним идентичные действия с помощью Ansible, для этого создадим на хостовой машине плейбук ~/task19/playbook.yaml и добавим в него следующие команды:</p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;- name: Set up NAT on inetRouter</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;template:&nbsp;</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;src: "{{ item.src }}"</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dest: "{{ item.dest }}"</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;owner: root</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;group: root</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode: "{{ item.mode }}"</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;with_items:</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- { src: "iptables_rules.ipv4", dest: </span></em><strong><em>"/etc/iptables_rules.ipv4"</em></strong><em><span style="font-weight: 400;">, mode: "0644" }</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- { src: "iptables_restore", dest: </span></em><strong><em>"/etc/network/if-pre-up.d/iptables"</em></strong><em><span style="font-weight: 400;">, mode: </span></em><strong><em>"0755"</em></strong><em><span style="font-weight: 400;"> }</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;when: (ansible_hostname == "inetRouter")</span></em></p>
<p><span style="font-weight: 400;">Модуль template копирует 2 файла, которые были указаны выше. Их тоже создаем здесь. Для файла <strong>/etc/network/if-pre-up.d/iptables</strong> уже установлен атрибут выполнения файла.</p>
<p><strong>Настройка маршрутизации транзитных пакетов с помощью Ansible</strong></p>
<p><span style="font-weight: 400;">В нашей схеме необходимо включить данную маршрутизацию на всех роутерах.</span></p>
<p><span style="font-weight: 400;">В Ansible есть специальный блок для внесений изменений в параметры ядра. Добавим его в плейбук:</span></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;- name: set up forward packages across routers</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;sysctl:</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;name: net.ipv4.conf.all.forwarding</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;value: '1'</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;state: present</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;when: "'routers' in group_names"</span></em></p>
<p><span style="font-weight: 400;">В условии указано, что изменения будут применяться только для группы &laquo;routers&raquo;, группа routers создана в hosts-файле:</span></p>
<p><strong><em>[routers]</em></strong></p>
<p><strong><em>inetRouter</em></strong><em><span style="font-weight: 400;"> ansible_host=192.168.50.10 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/inetRouter/virtualbox/private_key&nbsp;</span></em></p>
<p><strong><em>centralRouter</em></strong><em><span style="font-weight: 400;"> ansible_host=192.168.50.11 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/centralRouter/virtualbox/private_key&nbsp;</span></em></p>
<p><strong><em>office1Router</em></strong><em><span style="font-weight: 400;"> ansible_host=192.168.50.20 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/office1Router/virtualbox/private_key&nbsp;</span></em></p>
<p><strong><em>office2Router </em></strong><em><span style="font-weight: 400;">ansible_host=192.168.50.30 ansible_user=vagrant ansible_ssh_private_key_file=.vagrant/machines/office2Router/virtualbox/private_key</span></em></p>
<p><span style="font-weight: 400;">Файл hosts &mdash; это файл инвентаризации, в нем указан список серверов, их адреса, группы и способы доступа на сервер.</span></p>
<p><strong>Отключение маршрута по умолчанию с помощью Ansible</strong></p>
<p><span style="font-weight: 400;">При разворачивании нашего стенда Vagrant создает в каждом сервере свой интерфейс, через который у сервера появляется доступ в интернет. Отключить данный порт нельзя, так как через него Vagrant подключается к серверам. Обычно маршрут по умолчанию прописан как раз на этот интерфейс, данный маршрут нужно отключить.</span></p>
<p><span style="font-weight: 400;">Отключение дефолтного маршрута требуется настроить на всех хостах, кроме inetRouter.</span></p>
<p><span style="font-weight: 400;">Для отключения маршрута по умолчанию в файле </span><strong>/etc/netplan/00-installer-config.yaml</strong><span style="font-weight: 400;"> добавляем</span><span style="font-weight: 400;"> отключение маршрутов, полученных через DHCP</span><strong>:</strong></p>
<p><span style="font-weight: 400;"># This is the network config written by 'subiquity'</span></p>
<p><span style="font-weight: 400;">network:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;ethernets:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;eth0:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dhcp4: true</span></p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dhcp4-overrides:</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;use-routes: false</p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dhcp6: false</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;version: 2</span></p>
<p><span style="font-weight: 400;">Для выполнения идентичных изменений с помощью Ansible, можно воспользоваться следующим блоком:</span></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;- name: disable default route</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;template:&nbsp;</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;src: 00-installer-config.yaml</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dest: /etc/netplan/00-installer-config.yaml</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;owner: root</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;group: root</span></em></p>
<p><em><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode: 0644</span></em></p>
<p><em>&nbsp;&nbsp;&nbsp;&nbsp;when: (ansible_hostname != "inetRouter")</em></p>
<p><span style="font-weight: 400;">Добавим его в плейбук, также создадим файл 00-installer-config.yaml.</span></p>
<p><strong>Настройка статических маршрутов</strong></p>
<p><span style="font-weight: 400;">Для настройки статических маршрутов используется команда </span><strong>ip route</strong><span style="font-weight: 400;">.&nbsp;</span></p>
<p><span style="font-weight: 400;">Рассмотрим пример настройки статического маршрута на сервере office1Server. Исходя из схемы мы видим, что трафик с данного сервера будет идти через office1Router. Office1Server и office1Router у нас соединены через сеть managers (192.168.2.128/26). </span><strong>В статическом маршруте нужно указывать адрес следующего хоста.</strong><span style="font-weight: 400;"> Таким образом мы должны указать на сервере office1Server маршрут, в котором доступ к любым IP-адресам у нас будет происходить через адрес 192.168.2.129, который расположен на сетевом интерфейсе office1Router. Команда будет выглядеть так: </span><em><span style="font-weight: 400;">ip route add 0.0.0.0/0 via 192.168.2.129&nbsp;</span></em></p>
<p><strong>Маршруты, настроенные через команду ip route удаляются после перезагрузки или перезапуска сетевой службы.&nbsp;</strong></p>
<p><span style="font-weight: 400;">Для того, чтобы маршруты сохранялись после перезагрузки, нужно их указывать непосредственно в файле конфигурации сетевых интерфейсов.</span></p>
<p><span style="font-weight: 400;">В современных версиях Ubuntu для указания маршрута нужно поправить netplan-конфиг. Конфиги netplan хранятся в виде YAML-файлов и обычно лежат в каталоге </span><em><span style="font-weight: 400;">/etc/netplan</span></em></p>
<p><span style="font-weight: 400;">В нашем стенде такой файл - </span><strong>/etc/netplan/50-vagrant.yaml&nbsp;</strong></p>
<p><span style="font-weight: 400;">Для добавления маршрута, после раздела addresses нужно добавить блок:</span></p>
<p><strong>routes:</strong></p>
<p><strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- to: &lt;сеть назначения&gt;/&lt;маска&gt;</strong></p>
<p><strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;via: &lt;Next hop address&gt;</strong></p>
<p><span style="font-weight: 400;">Пример файла </span><span style="font-weight: 400;">/etc/netplan/50-vagrant.yaml</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="font-weight: 400;">&nbsp;---</span></p>
<p><span style="font-weight: 400;">network:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;version: 2</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;renderer: networkd</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;ethernets:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;enp0s8:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addresses:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 192.168.2.130/26</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>routes:</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- to: 0.0.0.0/0</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;via: 192.168.2.129</p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;enp0s19:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addresses:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 192.168.50.21/24</span></p>
<p><span style="font-weight: 400;">Важно помнить, что помимо маршрутов по умолчанию нужно будет использовать обратные маршруты.</span><span style="font-weight: 400;">&nbsp;</span></p>
<p><span style="font-weight: 400;">Разберем пример такого маршрута: допустим мы хотим отправить команду ping с сервера office1Server (192.168.2.130) до сервера centralRouter (192.168.0.1)&nbsp;</span></p>
<p><span style="font-weight: 400;">Наш трафик пойдёт следующим образом: </span><strong>office1Server &mdash; office1Router &mdash; centralRouter &mdash; office1Router &mdash; office1Server</strong></p>
<p><span style="font-weight: 400;">Office1Router знает сеть (192.168.2.128/26), в которой располагается сервер office1Server, а сервер centralRouter, когда получит запрос от адреса 192.168.2.130 не будет понимать, куда отправить ответ. Решением этой проблемы будет добавление обратного маршрута.&nbsp;</span></p>
<p><span style="font-weight: 400;">Обратный маршрут указывается так же, как остальные маршруты. Изучив схему, мы видим, что связь между сетями 192.168.2.0/24 и 192.168.0.0/24 осуществляется через сеть 192.168.255.10/30. Также мы видим что сети office1 подключены к centralRouter через порт eth5. На основании этих данных мы можем добавить маршрут в файл</span> <span style="font-weight: 400;">/etc/netplan/50-vagrant.yaml</span></p>
<p><span style="font-weight: 400;">eth5:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;addresses:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 192.168.255.9/30</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;routes:</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- to: 192.168.2.0/24</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;via: 192.168.255.10</p>
<p><span style="font-weight: 400;">Для настройки маршрутов с помощью Ansible нам необходимо подготовить файлы 50-vagrant.yaml с маршрутами для всех серверов. Далее с помощью модуля template мы можем их добавлять:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;- name: add default gateway for hosts</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;template:&nbsp;</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;src: "50-vagrant_</span><strong>{{ansible_hostname}}</strong><span style="font-weight: 400;">.yaml"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dest: /etc/netplan/50-vagrant.yaml</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;owner: root</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;group: root</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mode: 0644</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;- name: restart all hosts</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;reboot:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;reboot_timeout: 600</span></p>
<p><span style="font-weight: 400;">Последний блок перезагружает хосты. Для того, чтобы не писать 7 идентичных модулей, можно сделать один модуль, в котором будут перечисляться все хосты. Для этого у template-файлов должны быть идентичные имена формата </span><strong>50-vagrant_&lt;имя сервера&gt;.yaml</strong></p>
<p><span style="font-weight: 400;">Создадим такие файлы с настройками и поместим их сюда же. Будет 7 файлов.</span></p>
<p><span style="font-weight: 400;">На данном этапе настройка серверов закончена. После настройки серверов рекомендуется перезагрузить все хосты, чтобы проверить, что правила не удаляются после перезагрузки.&nbsp;</span></p>
<p><span style="font-weight: 400;">Помимо этого, рекомендуется на все хосты установить утилиту traceroute, для проверки нашего стенда.</span></p>
<p><span style="font-weight: 400;">Установка traceroute: </span><code>apt install -y traceroute</code></p>
<p><span style="font-weight: 400;">Можно добавить в плейбук (до перезагрузки) команду для установки пакета:</span></p>
<p>&nbsp; - name: install traceroute<br />&nbsp; &nbsp; ansible.builtin.apt:<br />&nbsp; &nbsp; &nbsp; name: traceroute<br />&nbsp; &nbsp; &nbsp; state: present<br />&nbsp; &nbsp; &nbsp; update_cache: yes</p>
<p><span style="font-weight: 400;">Для того, чтобы Ansible запускался сразу после развертывания серверов командой vagrant up, в текущий Vagrantfile нужно добавить блок запуска Ansible. Данный блок рекомендуется добавить после блока развертывания виртуальных машин:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if boxconfig[:vm_name] == "office2Server"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;box.vm.provision "ansible" do |ansible|</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ansible.playbook = "playbook.yml"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ansible.inventory_path = "hosts"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ansible.host_key_checking = "false"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ansible.limit = "all"</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end</span></p>
<p><span style="font-weight: 400;">При добавлении блока Ansible в Vagrant, Ansible будет запускаться после создания каждой ВМ, это создаст ошибку в разворачивании стенда и стенд не развернется. Для того, чтобы Ansible запустился после создания виртуальных машин, можно добавить условие, которое будет сравнивать имя виртуальной машины, и, когда условный оператор увидит имя последней созданной ВМ (office2Server), он запустит Ansible.&nbsp;</span></p>
<p><span style="font-weight: 400;">Разворачивание 7 виртуальных машин &mdash; процесс достаточно затратный для ресурсов компьютера, да и по времени тоже. При разворачивании стенда с помощью Ansible иногда могут вылетать ошибки из-за сетевой связности. Это не страшно, после того как ВМ будут созданы, можно просто ещё раз запустить процесс настройки через ansible с помощью команды:</span> <code>vagrant provision</code></p>




