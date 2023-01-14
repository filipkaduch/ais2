<script setup>
import { computed, ref } from 'vue'

const pdfText = ref('aaaa');
const isShownPic = ref(false);
const biggerBlocker = ref(false);
defineProps({
  msg: {
    type: String,
    required: true
  }
})

const date = computed(() => {
  return new Date().toLocaleString().replace(',','');
})

const keyboardMap = (event) => {
  switch (event.keyCode) {
    case 37:
      isShownPic.value = true;
      event.preventDefault();
      break;
    case 39:
      isShownPic.value = false;
      event.preventDefault();
      break;
    case 27:
      window.open('https://is.stuba.sk');
      break;
  }
};

window.addEventListener('keydown', keyboardMap);

function setPDF(pdfSource) {
  if (pdfSource === 'aaaa-combined') {
    biggerBlocker.value = true;
  } else {
    biggerBlocker.value = false;
  }
  pdfText.value = pdfSource;
}
</script>

<template>
  <img v-show="isShownPic" src="https://ais2.onrender.com/img.jpg" style="width: 100%; height: 100vh; display: none;" alt="panic" />
  <div id="hlavicka" @keydown.space="isShownPic = false" @keydown.esc="isShownPic = true">
    <div id="ie2">
      <div id="svatek">
        <span></span>
        {{ date }}
        <span></span>
        Rastislav
      </div>

      <div id="vlajky">

        <a href="https://is.stuba.sk/auth/elis/ot/psani_testu.pl?vysledky=1;detail=599403;lang=cz"></a>
        <img class="in-header" src="https://ais2.onrender.com/uisimg_154191.png" title="Česká verze">
        <a href="https://is.stuba.sk/auth/elis/ot/psani_testu.pl?vysledky=1;detail=599403;lang=sk"></a>
        <img class="in-header" src="https://ais2.onrender.com/uisimg_154224.png" title="Slovenská verzia">
      </div>
    </div>

    <div id="univerzita">Academic information system</div>

    <div id="menu">
      <div id="odkazy_fakult">
        <a @click="setPDF('ASOS-RT-21')">SvF</a> |
        <a @click="setPDF('ASOS_2021_RT')">SjF</a> |
        <a @click="setPDF('asos_2021_rt_firefox')">FEI</a> |
        <a @click="setPDF('ASOS_RT_21')">FCHPT</a> |
        <a @click="setPDF('asos_rt_21-22')">FAD</a> |
        <a @click="setPDF('ASOS_RT_2021')">MTF</a> |
        <a @click="setPDF('ASOS_RT_2021-2022')">FIIT</a> |
        <a @click="setPDF('mojaRT2021')">FEIIT</a> |
        <a @click="setPDF('skuska2021_RT_ASOS')">FIEIT</a> |
        <a @click="setPDF('SKUSKA_ASOS_21_RT_TZ')">EUBA</a> |
        <a @click="setPDF('skuskaASOS_21_RT')">NHF</a> |
        <a @click="setPDF('movehere')">AARCH</a> |
        <a @click="setPDF('aaaa-combined')">TOTAL</a> |
      </div>

      <div id="ikonky">
        <a href="?vysledky=1" title="Previous related page"></a>
        <a href="/auth" title="Back in application"></a>

        <a href="https://is.stuba.sk/auth/" title="Personal administration"></a>
        <a title="Application guide" href="/auth/help.pl?page=13768;back=aHR0cHM6Ly9pcy5zdHViYS5zay9hdXRoL2VsaXMvb3QvcHNhbmlfdGVzdHUucGw/dnlzbGVka3k9
MTtkZXRhaWw9NTk5NDAz
" class="context-help-invoke" target="_blank" data-contextHelpPage="13768"></a>
        <a href="/auth/system/logout.pl" title="Log out"></a>
      </div>

      <div id="ema">
        <a href="/auth/posta/" title="">411</a> <a href="/auth/posta/" title="">messages</a>
        <a href="/auth/dok_server/nove_dok.pl" title="">84</a> <a href="/auth/dok_server/nove_dok.pl" title="">documents</a>
        <a href="/auth/todo/" title="">0</a> <a href="/auth/todo/" title="">tasks</a>
      </div>


      <div id="log">
        Logged in:&nbsp;User
      </div>


    </div>
  </div>

  <div id="base">
    <div id="base-r">



      <div class="mainpage">
        <div><div><div><div><div><div><div style="width: 100%;"><div id="titulek"><h1>Do Test</h1><hr class="uisseparator" /></div><!--<table class="portal_menu"><tbody ><tr class="" ><td class="odsazena" nowrap="1" align="left"><a style="color: #831135" href="/auth/elis/ot/psani_testu.pl">Tests to do</a></td><td class="odsazena" nowrap="1" align="left"><b><a style="color: #831135" href="/auth/elis/ot/psani_testu.pl?vysledky=1">Submitted tests</a></b></td></tr></tbody></table><p />-->
          <div class="blocker" :class="biggerBlocker ? 'increase' : ''"></div>
          <div class="horizontal-blocker"></div>
          <div style="width: 100%; display: flex; justify-content: center; align-items: center">
            <iframe :src="`https://ais2.onrender.com/${pdfText}.pdf?#scrollbar=0&toolbar=0&navpanes=0&zoom=150`" type="application/pdf" width="100%" height="900px" />
          </div>
          <div class="blocker" :class="biggerBlocker ? 'increase' : ''" style="right: 0"></div>
          <form method="post" action="/auth/elis/ot/psani_testu.pl" enctype="application/x-www-form-urlencoded" name="check_ajax_form"><input type="hidden" name="correct_ajax" value="1" /></form><div class="pseudostrap-activated"></div></div></div></div></div></div></div></div><br /><ul id="navig-footer"><li><i><a style="color: #831135" href="?vysledky=1">Back to List of tests done</a></i></li><li><i><a style="color: #831135" href="/auth/elis/ot/psani_testu.pl">Back to List of tests to do</a></i></li><li><i><a style="color: #831135" href="/auth">Back to Personal administration</a></i></li></ul>
          <div class="timer"></div>
      </div>

    </div>
  </div>
  <div id="uis-control-data" data-uis_ang_lokalizace="US" data-cookiebar_cookie="uis_cookiebar_policy" data-stat_tel_predvolba="+421"></div>
</template>

<style type="text/css">table.elis_test_question {padding:0; position: relative} .editable-canvas-tooltip.active  {display: none}
div.baze_otazek-otazka, .baze_otazek-otazka td {padding:5px}
table.elis_test_question p, .elis_test_question p, .baze_otazek-otazka p {margin:0}
.vzorec_latex {vertical-align: middle}
.elis_test_question textarea {max-width: 100%; resize: vertical}
.elis_test_question td[valign=top] { vertical-align: middle}

.show_question_odpoved {width: 100%; overflow:auto; min-height: 50px;} .show_question_odpoved pre:not(.source) {  margin-top: 1rem; max-width: 90%; width: 800px; white-space: break-spaces; }
.podtrhnuto { border-bottom: 1px solid black; }

#hlavicka {
  position: relative;
  height: 170px;
  width: 100%;
  background-color: #831135;
  min-width: 940px;
}
#univerzita {
  color: #FFFFFF;
  text-align: right;
  font: 3em Tahoma, Verdana, Arial, sans-serif;
  padding: 3px 20px 7px 0;
  text-transform: uppercase;
}

#ikonky, #log, #ema {
  float: right;
  padding: 0 2px;
}

.horizontal-blocker {
  position: absolute;
  top: 48px;
  background-color: white;
  width: 100%;
  height: 32px;
  z-index: 2;
}

.timer {

}

.increase {
  width: calc((100% / 8) + 84px) !important;
}

#navig-footer {
  z-index: 3;
}

iframe { background-color:white; width: 100%; }

#odkazy_fakult {
  float: left;
  cursor: pointer;
}

.blocker {
  width: calc((100% / 8) + 104px) !important;
  z-index: 2;
  height: 100%;
  position: absolute;
  top: 48px;
  background-color: white;
}

#odkazy_fakult, #log, #ema {
  height: 25px;
  line-height: 25px;
  padding: 0 2px;
}

#menu {
  height: 25px;
  color: #c8c8db;
  padding: 0 5px;
  font-size: 11px;
  border-top: 1px solid #FFFFFF;
}

#ie2 {
  position: relative;
  height: 82px;
  background: url('@/components/uisimg_183025.png') no-repeat;
}

#svatek {
  position: absolute;
  right: 53px;
  top: 3px;
  color: #c8c8db;
}

#vlajky {
  position: absolute;
  right: 5px;
  top: 4px;
}

#base {
  margin: 0 5px;
  width: 100%;
}

#base-r {
  text-align: left;
}

h1 {
  font-size: 15px;
  margin: 5px 0 0 0;
  color: #831135;
  line-height: 21px;
  height: 21px;
  padding: 0 0 0 25px;
  border: 1px solid #c0c0c0;
  background: #e7ebed url('@/components/uisimg_183027.png') left top no-repeat;
}

.portal_menu {
  display: inline-block;
  vertical-align: bottom;
}

.portal_menu td:not(.active):not(.portal_menu_hole) {
  background: #fafafa;
  margin-top: 0.8rem;
}
.portal_menu td:not(.portal_menu_hole) {
  display: inline-block;
  border-top: solid 1px lightgray;
  border-left: solid 1px lightgray;
  border-right: solid 1px lightgray;
  border-bottom: solid 1px lightgray;
  border-radius: 8px 8px 0 0;
  padding: 0.4rem 1rem !important;
  min-height: 1.2rem;
  box-shadow: rgb(0 0 0 / 7%) 0px -1px 1px, rgb(0 0 0 / 7%) 0px -2px 2px;
  position: relative;
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
  vertical-align: bottom;
  height: 100%;
  transition: min-height .15s ease-in-out, margin-top .15s ease-in-out;
}
td.odsazena, td.zahlavi, th.zahlavi, tr.zahlavi > th, tr.zahlavi > td, tr.zahlavi > th.zahlavi, tr.zahlavi > td.zahlavi {
  padding-left: 0.6rem !important;
  padding-right: 0.6rem !important;
}
.portal_menu td {
  padding-right: 3rem!important;
}
td.odsazena, th.zahlavi {
  padding-left: 5px;
  padding-right: 5px;
}
td, th {
  padding-top: 0;
  padding-bottom: 0;
}

a, .fakelink {
  color: #831135;
  text-decoration: none;
}

hr.uisseparator {
  width: 80%;
  border: none;
  background: linear-gradient(to right, rgba(0,0,0,1) 0%, rgba(255,255,255,1) 100%);
  height: 1px;
  max-width: 80%;
  margin-bottom: 2rem;
  margin-left: 0;
}

</style>