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
