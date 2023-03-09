# EntornoDesarrollos
Repositorio destinado ha realizar un resumen de las entregas y los conceptos aprendidos durante el segundo trimestre en la asignatura de Entorno de Desarrollos
<br><h2>Entregar una automatizacion</h2>
Desarrolle una automatización con PowerShell centrada en el proyecto del anterior trimestre (aplicacion para el abono transporte) la cual consistía en una automatización de las notificaciones de información, de error y de avisos. 
````
   $appName = read-host "AppTransporte"
$notificationText = read-host "Su abono transporte caduca mañana"
$notificationTitle = read-host "Caducidad abono transporte"
$notificationType = read-host "WARNING"
$notificationType = $notificationType.ToUpper()
switch($notificationType){
    "INFO" {$notificationIcon = "info.png"}
    "WARNING" {$notificationIcon = "warning.png"}
    "ERROR" {$notificationIcon = "error.png"}
}
$notification = [pscustomobject]@{
    AppName=$appName
    NotificationText=$notificationText
    NotificationTitle=$notificationTitle
    NotificationType=$notificationType
    NotificationIcon=$notificationIcon
}
$notification | ConvertTo-Json | Out-File "$appName-notification.json"
Write-Host "Notification file created: $appName-notification.json"
````
<br><h2>Formularios</h2>
Realizamos formularios con PowerShell los cuales deberían tener ciertas peculiaridades como la **automatización**, el **guardado de datos en ficheros .txt**, o que **al pulsar en un botón de uno de los formularios se abriese otro formulario**.
<br>El formulario que yo desarrolle consistía en crear un primer formulario para introducir un correo electrónico y al pulsar el botón de guardar se abrirá otro donde se debería introducir la contraseña.Al pulsar el botón de guardar se guardaría todo lo introducido en un .txt
````
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName PresentationFramework

# correo electrónico
$emailForm = New-Object System.Windows.Forms.Form
$emailForm.Size = New-Object System.Drawing.Size(500,500)
$emailForm.StartPosition = [System.Windows.Forms.FormStartPosition]::CenterScreen
$emailForm.Text = "correo electrónico"

$emailTextBox = New-Object System.Windows.Forms.TextBox
$emailTextBox.Size = New-Object System.Drawing.Size(350,250)
$emailTextBox.Location = New-Object System.Drawing.Point(25,25)

$saveEmailButton = New-Object System.Windows.Forms.Button
$saveEmailButton.Size = New-Object System.Drawing.Size(100,50)
$saveEmailButton.Location = New-Object System.Drawing.Point(150,200)
$saveEmailButton.Text = "Guardar"

$saveEmailButton.Add_Click({
    $email = $emailTextBox.Text
    Set-Content -Path "C:\Users\laura\Desktop\Laura\DAM\Entorno\credentials.txt" -Value $email
    $emailForm.Close()

    # contraseña
    $passwordForm = New-Object System.Windows.Forms.Form
    $passwordForm.Size = New-Object System.Drawing.Size(400,300)
    $passwordForm.StartPosition = [System.Windows.Forms.FormStartPosition]::CenterScreen
    $passwordForm.Text = "Formulario de contraseña"

    $passwordTextBox = New-Object System.Windows.Forms.TextBox
    $passwordTextBox.Size = New-Object System.Drawing.Size(350,250)
    $passwordTextBox.Location = New-Object System.Drawing.Point(25,25)
    $passwordTextBox.PasswordChar = "*"

    $savePasswordButton = New-Object System.Windows.Forms.Button
    $savePasswordButton.Size = New-Object System.Drawing.Size(100,50)
    $savePasswordButton.Location = New-Object System.Drawing.Point(150,200)
    $savePasswordButton.Text = "Guardar"

    $savePasswordButton.Add_Click({
        $password = $passwordTextBox.Text
        Add-Content -Path "C:\Users\laura\Desktop\Laura\DAM\Entorno\credentials.txt" -Value $password
        $passwordForm.Close()
    })

    $passwordForm.Controls.Add($passwordTextBox)
    $passwordForm.Controls.Add($savePasswordButton)
    $passwordForm.ShowDialog()
})

$emailForm.Controls.Add($emailTextBox)
$emailForm.Controls.Add($saveEmailButton)
$emailForm.ShowDialog()
````
<br><h2>Diseño, realización de pruebas y optimización</h2>
Nos centramos en las pruebas de código,en la depuración de programas y en su optimización.
Durante la clase realizamos un ejercicio en el cual teniamos que optimizar al máximo posible un código.
El código de a continuación se divide en varias partes donde tenemos el código original sin la depuración realizada, y a continuación las siguientes pruebas y reformas que se le van haciendo
````
public class Beca {

    public static void main(String[] args) {
    //codigo original
        Scanner lecturaTeclado = new Scanner(System.in);
        int edad;
        System.out.println("Introduzca su edad");
        edad = lecturaTeclado.nextInt();*/
        if (edad<=30){
            if (edad>5){
                System.out.println("puedes optar a la beca");
            }else
                System.out.println("Puedes optar a la beca si sabes leer");
        }else
            System.out.println("no puedes");*/

        //operador ternario
   //primera depuración
       switch ((0 <= edad && edad <= 24) ? 0 : (25 <= edad && edad <= 30) ? 1 : 2) {
            case 0:
                System.out.println("puedes optar a la beca si sabes leer");
                break;
            case 1:
                System.out.println("puedes optar a la beca");
                break;
            case 2:
                System.out.println("no puedes optar a la beca");
                break;
        }
   //resultado final
        pedirEdad(5);
    }
    public static void pedirEdad(int repeticion) {
        Scanner teclado = new Scanner(System.in);
        int edad;
        for (int i = 0; i < repeticion; i++) {
            System.out.println("Introduzca su edad");
            edad = teclado.nextInt();
            switch ((0 <= edad && edad <= 24) ? 0 : (25 <= edad && edad <= 30) ? 1 : 2) {
                case 0:
                    System.out.println("puedes optar a la beca si sabes leer");
                    break;
                case 1:
                    System.out.println("puedes optar a la beca");
                    break;
                case 2:
                    System.out.println("no puedes optar a la beca");
                    break;
            }
        }
    }
}
````
