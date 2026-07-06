Para poder usar el modulo de actualizaciones de windows es necesario poder usar el modulo:

Si tienes internet:
ansible-galaxy collection install ansible.windows

si no tienes conexion a internet, descargar el .tar:
https://galaxy.ansible.com/ui/repo/published/ansible/windows/

instalar el modulo:
# Suponiendo que el fichero está en tu directorio actual
ansible-galaxy collection install ansible-windows-2.2.0.tar.gz

# O proporcionando la ruta completa
ansible-galaxy collection install /ruta/completa/a/ansible-windows-2.2.0.tar.gz

explicación del Playbook
hosts: windows: Este playbook se ejecutará en todos los servidores que pertenezcan al grupo windows en tu fichero de inventario de Ansible.
name: Instalar actualizaciones...: Es el nombre de la tarea que se mostrará durante la ejecución del playbook.
ansible.windows.win_updates: Este es el módulo de Ansible que se encarga de gestionar las actualizaciones de Windows.
category_names: Aquí especificas qué tipo de actualizaciones quieres instalar. En este ejemplo, estamos instalando SecurityUpdates (Actualizaciones de seguridad), CriticalUpdates (Actualizaciones críticas) y UpdateRollups (Paquetes acumulativos de actualizaciones). Puedes ajustar esta lista según tus necesidades.
reboot: yes: ¡Importante! Esta opción reiniciará automáticamente el servidor si una o más de las actualizaciones instaladas lo requieren. Si no quieres que el servidor se reinicie automáticamente, cambia este valor a no.
log_path: C:\temp\ansible_win_updates.log: Guarda un registro detallado de la operación de actualización en el fichero especificado en el servidor Windows.
register: update_result: Guarda la salida del módulo win_updates en una variable llamada update_result. Esto nos permite usar la información de la salida en tareas posteriores.
name: Mostrar los KB que requieren reinicio: Esta es una tarea de depuración que se ejecuta solo si se necesita un reinicio (when: update_result.reboot_required). Imprime una lista de los números de KB de las actualizaciones que han provocado la necesidad de reiniciar.

# Ejecucion del playbook en linea de comandos:
ansible-playbook -i inventario.ini nombre-playbook.yml
