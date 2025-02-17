---
title: グッドプラクティスの共有
---

<!--  Source codes of css and javascript were from https://www.tam-tam.co.jp/tipsnote/javascript/post14636.html. Thank you for the great codes -->

<style type="text/css">

.search-box_label {
    font-weight: bold;
}
.is-hide {
    display: none;
}

</style>


<script type="text/javascript">

var searchBox = '.search-box'; // 絞り込む項目を選択するエリア
var listItem = '.list_item';   // 絞り込み対象のアイテム
var hideClass = 'is-hide';     // 絞り込み対象外の場合に付与されるclass名

$(function() {
    // 絞り込み項目を変更した時
    $(document).on('change', searchBox + ' input', function() {
        search_filter();
    });
});

/**
 * リストの絞り込みを行う
 */
function search_filter() {
    // 非表示状態を解除
    $(listItem).removeClass(hideClass);
    for (var i = 0; i < $(searchBox).length; i++) {
        var name = $(searchBox).eq(i).find('input').attr('name');
        // 選択されている項目を取得
        var searchData = get_selected_input_items(name);
        // 選択されている項目がない、またはALLを選択している場合は飛ばす
        if(searchData.length === 0 || searchData[0] === '') {
            continue;
        }
        // リスト内の各アイテムをチェック
        for (var j = 0; j < $(listItem).length; j++) {
            // アイテムに設定している項目を取得
            var itemData = get_setting_values_in_item($(listItem).eq(j), name);
            // 絞り込み対象かどうかを調べる
            var check = array_match_check(itemData, searchData);
            if(!check) {
                $(listItem).eq(j).addClass(hideClass);
            }
        }
    }
}

/**
 * inputで選択されている値の一覧を取得する
 * @param  {String} name 対象にするinputのname属性の値
 * @return {Array}       選択されているinputのvalue属性の値
 */
function get_selected_input_items(name) {
    var searchData = [];
    $('[name=' + name + ']:checked').each(function() {
        searchData.push($(this).val());
    });
    return searchData;
}

/**
 * リスト内のアイテムに設定している値の一覧を取得する
 * @param  {Object} target 対象にするアイテムのjQueryオブジェクト
 * @param  {String} data   対象にするアイテムのdata属性の名前
 * @return {Array}         対象にするアイテムのdata属性の値
 */
function get_setting_values_in_item(target, data) {
    var itemData = target.data(data);
    if(!Array.isArray(itemData)) {
        itemData = [itemData];
    }
    return itemData;
}

/**
 * 2つの配列内で一致する文字列があるかどうかを調べる
 * @param  {Array} arr1 調べる配列1
 * @param  {Array} arr2 調べる配列2
 * @return {Boolean}    一致する値があるかどうか
 */
function array_match_check(arr1, arr2) {
    // 絞り込み対象かどうかを調べる
    var arrCheck = false;
    for (var i = 0; i < arr1.length; i++) {
        if(arr2.indexOf(arr1[i]) >= 0) {
            arrCheck = true;
            break;
        }
    }
    return arrCheck;
}

</script>
## お知らせ

- 2020年9月22日 新しい記事を公開しました．

## はじめに
* このページは，本学で行われたオンライン授業のグッドプラクティスを共有するためのページです．  
* オンライン授業に関する学生アンケートに設置されていた「やり方の良かった授業」の自由記述欄において，多くのポジティブなコメントが寄せられていた先生方へのインタビュー記事が掲載されています．
* 2020年9月21日現在，14名の先生方にインタビューをし終わった状況で，記事を順次公開予定です．
* これらの情報がみなさまの実践の参考になれば幸いです．

## 記事一覧
以下のチェックボックスを使うことで記事の絞り込みができます．<br>

<form>
    <div class="search-box">
        <span class="search-box_label">形態:</span>
        <input type="checkbox" name="format" value="realtime_online">リアルタイム（オンライン）　
        <input type="checkbox" name="format" value="ondemand">オンデマンド　
    </div>
    <div class="search-box">
        <span class="search-box_label">学生数:</span>
        <input type="checkbox" name="number" value="lt30">30名以下　
        <input type="checkbox" name="number" value="mt30-lt100">31名～100名　
        <input type="checkbox" name="number" value="mt100">101名以上　
    </div>
    <div class="search-box">
        <span class="search-box_label">ツール:</span>
        <!-- <input type="checkbox" name="tool" value="">全て -->
        <input type="checkbox" name="tool" value="itc-lms">ITC-LMS　
        <input type="checkbox" name="tool" value="google-classroom">Google Classroom　
        <input type="checkbox" name="tool" value="slack">Slack　<br>
        　　　<input type="checkbox" name="tool" value="zoom">Zoom　
        <input type="checkbox" name="tool" value="webex">Webex　
        <input type="checkbox" name="tool" value="google-meet">Google Meet　<br>
        　　　<input type="checkbox" name="tool" value="google-document">Google Document　
        <input type="checkbox" name="tool" value="google-sheets">Google Sheets　
        <input type="checkbox" name="tool" value="google-slides">Google Slides　
        <input type="checkbox" name="tool" value="google-forms">Google Forms<br>
        　　　<input type="checkbox" name="tool" value="slido">Slido　<br>
    </div>
    <div class="search-box">
        <span class="search-box_label">タグ:</span>
        <input type="checkbox" name="keyword" value="hand-writing">板書　
        <input type="checkbox" name="keyword" value="experiment">実験・実習　
        <input type="checkbox" name="keyword" value="group-work">グループワーク　
    </div>
</form>  
  
<ul class="list">  
<br>
    <li class="list_item" data-format='["realtime_online", "ondemand"]' data-number='lt30' data-tool='["zoom", "slido", "google-document", "google-sheets", "google-slides", "google-forms", "google-classroom"]' data-keyword='["group-work"]'>
        <a href="./interview/kurita">栗田佳代子 先生の授業: 「学びの場」づくり（教育学部 20名程度）</a><br>
        <ul>
            <li>ポイント: リアルタイムとオンデマンドの組み合わせ　グループワーク</li>
            <li>利用ツール: Google Classroom, Zoom, Slido, Google Documents, Sheets, Slides, Forms</li>
        </ul>
    </li>
    <!--
    <li class="list_item" data-format='["realtime_online"]' data-number='mt30-lt100' data-tool='["slido", "google-document", "google-sheets", "google-slides", "google-forms", "google-classroom"]' data-keyword='["group-work"]'>
        <a href="./kurita">栗田佳代子 先生・「学びの場」づくり（教育学部）</a><br>
        <ul>
            <li>約80名履修　リアルタイム　グループワーク</li>
            <li>利用ツール: Slido, Google Documents, Sheets, Slides, Forms, Google Classroom</li>
        </ul>
    </li>
    <li class="list_item" data-format='["ondemand"]' data-number='mt100' data-tool='["zoom", "slido", "google-slides", "google-forms", "google-classroom"]' data-keyword='["group-work"]'>
        <a href="./kurita">栗田佳代子 先生・「学びの場」づくり（教育学部）</a><br>
        <ul>
            <li>約120名履修　オンデマンド　グループワーク</li>
            <li>利用ツール: Zoom, Slido, Slides, Forms, Google Classroom</li>
        </ul>
    </li>
    -->

</ul>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
