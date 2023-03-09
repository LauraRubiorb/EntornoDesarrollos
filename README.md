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
El formulario que yo desarrolle consistía en crear un primer formulario para introducir un correo electrónico y al pulsar el botón de guardar se abrirá otro donde se debería introducir la contraseña.Al pulsar el botón de guardar se guardaría todo lo introducido en un .txt
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
