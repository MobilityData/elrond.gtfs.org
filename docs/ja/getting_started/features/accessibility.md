# アクセシビリティ 
 アクセシビリティ機能は、障害のある人がサービスを利用するために必要な情報を提供することを目的としています。 
 
## 停留所の車椅子アクセシビリティ 
 
 停留所の車椅子アクセシビリティを使用すると、指定した場所から車椅子での乗車が可能かどうかを示すことができます。車椅子を使用する乗客にサービスを提供するには、車椅子での乗車が可能であることを指定することは、tであることを指定するのと同じくらい重要です。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`wheelchair_boarding` | 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 - [場所の種類](../base_add-ons/#location-types) 出入口や乗車エリアなどの駅の場所のアクセシビリティ情報を定義する場合。 
 
 ??? `サンプルデータ`の注記 
 
<p style="font-size:16px"> 
 次のサンプルは、`wheelchair_boarding=1` を使用して、停留所 `TAS001` で車椅子での乗車が可能であることを示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | location_type | wheelchair_boarding | 
 |---------|------------|------------|------------|---------------|----------------------| 
 | TAS001 | 5 Av/53 St | 40.760167 |-73.975224 | | 1 | 
 
 
## Trips Wheelchair Accessibility 
 
 Trips Wheelchair Accessibility を使用すると、vehicleが車椅子を使用する乗客に対応できるかどうかを示すことができます。車椅子を使用する乗客の役に立つためには、vehicleが車椅子を使用する乗客に対応できることを指定することは、vehicleが対応できtことを指定するのと同じくらい重要です。乗客が特定の停留所で旅行にアクセスできるようにするには、停留所と旅行の両方が車椅子でアクセス可能である必要があります。
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-----------------------------------| 
 |[trips.txt](../../../documentation/schedule/reference/#tripstxt)|`wheelchair_accessible `| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? note "サンプル データ" 
 
<p style="font-size:16px"> 
 次のサンプルは、旅行` AWE1 `で使用されるvehicleには少なくとも 1 台の車椅子を収容できる装備があり、旅行` AWE2 `で使用されるvehicleにはそれがないことを示しています。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#tripstxt"><b>trips.txt</b></a><br> 
</p> 
 
 | route_id | service_id | trip_id | wheelchair_accessible | 
 |----------|-----------|---------|-----------------------| 
 | RA | WE | AWE1 | 1 | 
 | RA | WE | AWE2 | 2 | 
 
 
## テキスト読み上げ 
 
 テキスト読み上げを使用すると、テキストを音声に変換するために必要な入力を提供できます。これにより、支援技術を使用してテキストを読み上げる乗客が、交通サービスを利用するときに正しい停留所名を取得できるようになります。 
 
 | 含まれるファイル | 含まれるフィールド | 
 |----------------------------------|-------------------| 
 |[stops.txt](../../../documentation/schedule/reference/#stopstxt)|`tts_stop_name| 
 
 **前提条件**: 
 
 - [基本機能](../base) 
 
 ??? 注記`サンプルデータ` 
 
<p style="font-size:16px"> 
 次のサンプルは、停留所名の読み上げ可能なバージョンを提供しており、テキスト読み上げツールで名前を読み上げることができます。
</p> 
 ！！！ 注記 "" 
<p style="font-size:16px"> 
 <a href="../../../documentation/schedule/reference/#stopstxt"><b>stops.txt</b></a><br> 
</p> 
 
 | stop_id | stop_name | stop_lat | stop_lon | tts_stop_name | 
 |---------|-------------|-------------|-------------|---------------------------| 
 | TAS001 | 5 Av/53 St | 45.5035680 |-73.587079 | 5番街と53番街 | 
 

