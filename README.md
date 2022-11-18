# WebinyBP
Introduccion:

Este repositorio contiene todo lo necesario para hacer un deploy de Webiny con pulumi en un S3 y usando DynamoDB solamente.
Configurado para la region "us-east-1" pero es posible cambiar desde el .env así como el backend de pulumi.

Requisitos:

- Instalar Node>14 
- yarn 1.22.0 || >= 2 
- Cuenta AWS y Credenciales de usuario (En las instrucciones se especifica como configurar las credenciales)
- El proceso de instalación requiere 4GB de RAM


Deploy:

1. yarn install

2. HACER CREDENCIALES AWS:

Paso por paso oficial:
https://www.webiny.com/docs/infrastructure/aws/configure-aws-credentials

Pasos en español:

Configurar credenciales AWS https://www.webiny.com/docs/infrastructure/aws/configure-aws-credentials

-Para crear su cuenta de AWS y configurar sus credenciales de IAM, primero debemos navegar a la página de la consola de AWS : https://aws.amazon.com/es/console/ -A continuación, haga clic en Create a new AWS account -Ahora ingrese sus credenciales y cree su cuenta

-Una vez que esté registrado, inicie sesión y diríjase a la Consola de administración de AWS y seleccione 'IAM' en 'Security, Identity & Compliance' -Haga click en 'IAM' y seleccione 'Usuarios' en 'Gestión de acceso' -Haga click en Agregar usuario para crear la cuenta con las credenciales de IAM

-Aquí ingresa a un proceso de 5 pasos, y el primer paso es crear un nombre de usuario para las credenciales

Elija el nombre de usuario y seleccione la casilla de verificación Acceso programático antes de pasar al siguiente paso.

En el siguiente paso, defina el nivel de acceso para el nuevo usuario. Seleccione 'Adjuntar políticas existentes' de las tres opciones disponibles. Luego seleccione la política 'AdministratorAccess' marcando la casilla de verificación junto a ella. Cuando esté listo, haga clic en el botón Siguiente

En caso de que no desee agregar ninguna etiqueta a su nuevo usuario, puede omitir este paso y hacer clic en el botón Siguiente

Después de completar todos los pasos, verá una página a Revisar. Si todo es correcto, haga clic en el botón Crear usuario.

Por último, recibirá un mensaje de éxito con su ID de clave de acceso y clave de acceso secreta. Debe copiar estas cadenas y mantenerlas seguras, ya que las necesita para el siguiente paso. Una vez que salga de esta pantalla, ya no podrá ver las credenciales. Si los pierde, deberá eliminar el usuario y crear uno nuevo.*

-Alternativamente, también puede definir una política detallada utilizando nuestra plantilla de CloudFormation que creará un grupo de usuarios con todas las políticas necesarias para su proyecto

La creación del recurso tardará unos minutos. Después de completar, verá los registros con CREATE_COMPLETE

3. Hacer un .env como el del example

4. Hacer un bucket vacio en la misma region que esta definido en el .env y colocarlo en la variable "WEBINY_PULUMI_BACKEND"

5. YARN WEBINY DEPLOY

El proceso puede llegar a tardar hasta 20 minutos.

Recordatorio: hay que crear el user en cognito, luego verificarlo, luego tomar el sub y crear 2 items en dynamo, el user en cuestion y el permiso.


Uninstall: 
Para desinstalar todo lo relacionado con Webiny, en la misma terminal ejecutar estos comandos uno por uno y en el mismo orden.

1. yarn webiny destroy apps/website --env dev
2. yarn webiny destroy apps/admin --env dev
3. yarn webiny destroy apps/api --env dev
4. yarn webiny destroy apps/core --env dev

El proceso puede llegar a tardar hasta 20 minutos.

Esto elimina toda la infraestructura en AWS. El comando webiny destroy esta ejecutando un pulumi destroy junto con otros comandos.
