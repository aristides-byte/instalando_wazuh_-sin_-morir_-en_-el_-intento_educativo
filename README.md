# instalando_wazuh_sin_morir_en_el_intento_educativo

Instalación de Wazuh

Este proyecto corresponde a la instalación y configuración de Wazuh como sistema de detección de intrusos (SIEM), integrando agentes en servidores Windows y Linux para la recolección y análisis de logs.

1. Instalación de máquinas virtuales

Windows Server → Instalado y configurado como host para pruebas. (ayuda en caso de necesitarla https://tinyurl.com/26wwfgke), recuerda generar una politica de seguridad en el firewall de windows que permita todo el trafico, tambien valida con el comando ping entre servidor y cliente para la conectividad.

Ubuntu → Instalado como sistema complementario. (ayuda en caso de necesitarla https://tinyurl.com/2crbg6fg)

Ubuntu con Wazuh Server → Instalado con el siguiente comando en la terminal:

curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a

Una vez terminada la intalacion ya puedes acceder a wazuh, recuerda que a ip de tu server ubuntu es la que debes ingresar a tu navegador: 

<img width="940" height="429" alt="image" src="https://github.com/user-attachments/assets/123c0a36-46a5-4296-ba75-8aaa0f981260" />

2. Si tienes problemas para recordar la contraseña te dejo el siguiente comando para verla nuevamente:

sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt

3. Para poder escanear la maquina donde esta alojada wazuh dejo la siguiente ruta a modificar:

Edita /var/ossec/etc/internal_options.conf

    sudo nano /var/ossec/etc/internal_options.conf

- Busca la línea:
    
    vulnerability-detection.disable_scan_manager=1
    
- Cambia el valor a 0:
    
    `vulnerability-detection.disable_scan_manager=0
    
Reinicia Wazuh-Manager

sudo systemctl restart wazuh-manager

<img width="940" height="437" alt="image" src="https://github.com/user-attachments/assets/cd54cc14-bb6f-441e-9728-f3ffd1bdfa52" />

Esta imagen muestra que ya estamos revisando el estado del server:

<img width="940" height="488" alt="image" src="https://github.com/user-attachments/assets/2534ba5d-3505-4608-9bc3-1b119676c8e1" />

4. Instalación de Wazuh Agent en el Servidor Windows Server

  Recuerda que si no has realizado la configuracion de regla en el firewall para permitir el trafico y no tienes ping entre el cliente y servidor el agente no estara operativo.

Para la instalación del agente en Windows se utiliza el siguiente comando generado por wazuh para la instalación del agente via powershell o cmd:

Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.12.0-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='ip server' WAZUH_AGENT_NAME='nombre de la maquina'

<img width="940" height="136" alt="image" src="https://github.com/user-attachments/assets/e022d536-3fb6-4f80-8015-3225762b3f43" />

En la línea de WAZUH_AGENT_NAME='' se debe agregar el nombre de la maquina

Una vez ejecutado el comando se genera el proceso de instalación una vez terminado se ejecuta el siguiente comando:

NET START WazuhSvc: esto valida que el servicio de wazuh este habilitado.

5.	Configurar Wazuh Agent para que se conecte con el servidor SIEM. (2 puntos) 

Una vez instalado el agente se valida que este conectado al servidor SIEM:

<img width="940" height="385" alt="image" src="https://github.com/user-attachments/assets/70facc94-12cd-4abe-bfe2-5930105c2077" />

<img width="940" height="387" alt="image" src="https://github.com/user-attachments/assets/cfc42b65-3656-408b-90d3-9bec6a1ae983" />


Un Saludo y feliz dia.




   


