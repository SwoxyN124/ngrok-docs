<?php
//error_reporting(0);

       $isimad = $_GET['ad'];
       $soyad = $_GET['soyad'];

        if (empty($isimad)) {
            echo json_encode(["success" => "false", "message" => " Ad Oyunda Hata vardir lutfen bekleyiniz", "Api_Owner" => "Krex & Swoxy"], JSON_PRETTY_PRINT);
            die();
        }

        if (empty($soyad)) {
            echo json_encode(["success" => "false", "message" => " Soyad Oyunda Hata vardir lutfen bekleyiniz", "Api_Owner" => "Krex & Swoxy"], JSON_PRETTY_PRINT);
            die();
        }

        $url = "xd/adsoyad.php?ad=$isimad&soyad=$soyad";

$con = mysqli_connect("localhost", "root", "", "101m");
$response = array();
if ($con) {
    $sql = "SELECT * FROM `101m` WHERE ADI='$isimad' AND SOYADI='$soyad'";
    $result = mysqli_query($con, $sql);
    if ($result) {

        header("Content-type: application/json; charset=utf-8");
        $idk=0;
        while($row = mysqli_fetch_assoc($result)) {
            $response[$idk]['jevo_TC'] = $row['TC'];
            $response[$idk]['jevo_ADI'] = $row['ADI'];
            $response[$idk]['jevo_SOYADI'] = $row['SOYADI'];
            $response[$idk]['jevo_DOGUMTARIHI'] = $row['DOGUMTARIHI'];
            $response[$idk]['jevo_NUFUSIL'] = $row['NUFUSIL'];
            $response[$idk]['jevo_NUFUSILCE'] = $row['NUFUSILCE'];
            $response[$idk]['jevo_ANNEADI'] = $row['ANNEADI'];
            $response[$idk]['jevo_ANNETC'] = $row['ANNETC'];
            $response[$idk]['jevo_BABAADI'] = $row['BABAADI'];
            $response[$idk]['jevo_BABATC'] = $row['BABATC'];
            $response[$idk]['jevo_UYRUK'] = $row['UYRUK'];
            $idk++;
        }


        
        echo json_encode($response, JSON_UNESCAPED_UNICODE); //, JSON_PRETTY_PRINT

        $api = curl_init($url);
        curl_setopt($api, CURLOPT_URL, $url);
        curl_setopt($api, CURLOPT_RETURNTRANSFER, true);
    }
}
else {
    echo "Hata var :d";
}
?>
