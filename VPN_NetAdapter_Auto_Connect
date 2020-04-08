while(1){
    if(Test-Connection  8.8.8.8 -Quiet){
        Write-Host "Internet Connected." -ForegroundColor "Green"
        if (Test-Connection  <private_ip> -Quiet) { 
            Write-Host "VPN Connected." -ForegroundColor "Green" 
        }else{
            Write-Host "VPN Not Connected." -ForegroundColor "Red"

            $vpnName = "VPN Adapter connection";
            $vpn = Get-VpnConnection -Name $vpnName;
            $count = 1;
            while($vpn.ConnectionStatus -eq "Disconnected"){
                rasdial $vpnName "username" "password";
                Start-Sleep -Seconds 10
                if($count -eq 2){
                    break;
                }
                $count++;
            }
        }
    }else{
        $vpnName = "VPN Adapter connection";
        $vpn = Get-VpnConnection -Name $vpnName;
        Write-Host "Internet Not Connected." -ForegroundColor "Red"
        rasdial $vpnName /DISCONNECT;
        Write-Host "VPN Is Disconnected." -ForegroundColor "Red"
        netsh wlan disconnect interface="*"
        netsh wlan connect ssid=ssid_name name=ssid_name/profile_name interface="Wi-Fi"
                
    }
}
