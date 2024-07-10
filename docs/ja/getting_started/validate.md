# GTFSフィードの品質を評価する 
 
 高品質のGTFS は完全かつ正確で、最新のものです。つまり、サービスの現在の運用状況が反映され、可能な限り多くの情報が提供されます。 
 
## 完全なデータ 
 
 高品質のGTFSには、休日や夏季のスケジュール変更、正確な停車場所、routes名や乗客向け資料と一致する行先標識など、重要なサービス詳細が含まれます。agencyがベンダーと協力してGTFSを作成する場合でも、印刷物、車内、オンラインで提示される情報の一貫性を確保するのは最終的にはagencyの責任です。 
 
## 正確なデータ 
 
 正確なデータは、信頼性が高く使いやすい交通機関の利用者にサービスを提供するために不可欠です。データにエラーがあると、データセットの一部または全体が使用できなくなる可能性があります。 
 
## 最新データ 
 
 古いデータは、フィードが利用できないよりも問題になることがあります。情報を公開するだけでは不十分で、乗客が見て体験するものと一致している必要があります。最大手の交通機関の中には、 GTFSを毎週、あるいは毎日更新しているところもありますが、ほとんどの機関は数か月ごと、またはサービスが変更される年に数回、 GTFSを更新する必要があります。これには、新しいroutesやstops、時刻表の変更、運賃体系の更新などが含まれます。 
 
 多くの機関は、 GTFSの作成と管理をベンダーに依頼しています。サービスの変更について積極的に問い合わせてくるベンダーもいますが、機関が今後のサービスの変更についてベンダーとコミュニケーションを取ることが重要です。サービスの変更を事前にGTFSに反映させることで、機関、ベンダー、旅行プランナー、乗客の全員にとって移行がスムーズに進むようにすることができます。 
 
## 公式検証ツールの使用 
 
 公式GTFS検証ツールは、データセットの品質を公式仕様に照らして評価し、業界内で何が高品質のデータセットを構成するかについて共通の理解を確保します。
 
 [MobilityData](https://mobilitydata.org/) が管理する無料のオープンソース [Canonical GTFS Schedule検証ツール](https://gtfs-validator.mobilitydata.org/)[^1] は、 GTFSデータが公式の [GTFS Schedule Reference](../../documentation/schedule/reference/) および [ベスト プラクティス](../../documentation/schedule/schedule_best_practices) に準拠していることを確認します。他の関係者と共有できる使いやすいレポートと包括的なドキュメントを提供します。
 
<div class="usage"> 
<div class="usage-list"> 
<ol> 
<li> <a href="https://gtfs-validator.mobilitydata.org/">gtfs-validator.mobilitydata.org</a>にアクセスしてください。</li> 
<li> GTFSデータセットを読み込みます。ZIP ファイルを選択またはドラッグ アンド ドロップするか、 URLをコピー/貼り付けることができます。</li> 
<li>検証が完了すると、レポートを開くオプションが提供されます。</li> 
<li>検証ツールがデータに問題を発見したかどうか、また、その修正方法に関するドキュメントへのリンクが表示されます。検証レポートのURL は30 日間有効で、他のユーザーと共有できます。</li> 
</ol> 
</div> 
<div class="usage-video"> 
<video class="center" width="560" height="315" controls> 
<source src="../../assets/validator_demo_large.mp4" type="video/mp4"> 
</video> 
</div> 
</div> 
 
 同様に、無料かつオープンソースの正規の [GTFS Realtime検証ツール](https:) を使用すると、 GTFSデータが公式の [GTFS Realtimeリファレンス](../../documentation/realtime/reference/) および [ベスト プラクティス](../../documentation/realtime/realtime_best_practices) に準拠していることが保証されます。 
 
 高品質なデータの作成については、[カリフォルニア交通データガイドライン](https://dot.ca.gov/cal-itp/california-transit-data-guidelines)、[GTFSGTFS Scheduleのベストプラクティス](../../documentation/schedule/schedule_best_practices)、[GTFS Realtimeのベストプラクティス](../../documentation/realtime/realtime_best_practices)をご覧ください。
 
 [^1]: このツールをデータパイプラインで使用し、このプロジェクトに貢献する方法の詳細については、[GitHubリポジトリ](https://github.com/MobilityData/gtfs-validator)をご覧ください。
 

