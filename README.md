# Seerat<!DOCTYPE html>
<html lang="ur">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Seerat AI v4 Pro</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;}
body{background:#1a0a2e;min-height:100vh;font-family:Arial,sans-serif;color:white;}

#setupScreen{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;padding:30px 20px;background:linear-gradient(180deg,#2d1554,#1a0a2e);}
#setupScreen h1{font-size:26px;color:#ff6b9d;margin-bottom:8px;text-align:center;}
#setupScreen p{font-size:13px;color:rgba(255,255,255,0.6);text-align:center;margin-bottom:24px;line-height:1.6;direction:rtl;}
.sbox{width:100%;max-width:380px;background:rgba(255,255,255,0.08);border:1px solid rgba(255,107,157,0.3);border-radius:16px;padding:22px;}
.lbl{font-size:12px;color:rgba(255,255,255,0.6);margin-bottom:6px;display:block;direction:rtl;}
.inp{width:100%;background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.3);border-radius:10px;padding:12px 14px;color:white;font-size:13px;margin-bottom:14px;outline:none;}
.inp:focus{border-color:#ff6b9d;}
.sbtn{width:100%;padding:14px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;border-radius:12px;color:white;font-size:15px;font-weight:bold;cursor:pointer;}
.skipbtn{background:none;border:none;color:rgba(255,255,255,0.3);font-size:12px;margin-top:14px;cursor:pointer;text-decoration:underline;display:block;text-align:center;width:100%;}
.saved-note{font-size:11px;color:#00ff88;text-align:center;margin-top:10px;direction:rtl;}

#mainApp{display:none;flex-direction:column;min-height:100vh;}

.hdr{background:linear-gradient(180deg,#2d1554,#1a0a2e);padding:12px 16px 10px;text-align:center;border-bottom:1px solid rgba(255,107,157,0.2);position:relative;}
.av-wrap{position:relative;width:70px;height:70px;margin:0 auto 6px;}
.av{width:70px;height:70px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:30px;border:3px solid #ff6b9d;overflow:hidden;cursor:pointer;}
.av img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.av-edit{position:absolute;bottom:0;right:0;width:22px;height:22px;background:#ff6b9d;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;cursor:pointer;border:2px solid #1a0a2e;}
#avatarInput{display:none;}
.nm{font-size:20px;font-weight:bold;color:#ff6b9d;letter-spacing:2px;}
.nm2{font-size:12px;color:#d7bde2;margin-top:2px;direction:rtl;}
.st{display:flex;align-items:center;justify-content:center;gap:6px;margin-top:4px;font-size:11px;color:rgba(255,255,255,0.5);}
.dot{width:7px;height:7px;background:#00ff88;border-radius:50%;animation:pulse 2s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:0.4;}}
.wake-txt{font-size:10px;color:rgba(255,107,157,0.6);margin-top:2px;}
.resetbtn{font-size:10px;color:rgba(255,107,157,0.5);background:none;border:1px solid rgba(255,107,157,0.2);border-radius:20px;padding:3px 10px;cursor:pointer;margin-top:4px;}

/* INFO BAR - Weather/Namaz */
.infobar{display:flex;gap:0;border-bottom:1px solid rgba(255,107,157,0.15);}
.icard{flex:1;padding:8px 6px;text-align:center;background:rgba(255,255,255,0.03);cursor:pointer;border:none;color:white;}
.icard:first-child{border-right:1px solid rgba(255,107,157,0.15);}
.icard-ico{font-size:16px;}
.icard-val{font-size:11px;font-weight:bold;color:#ff6b9d;margin-top:2px;}
.icard-lbl{font-size:9px;color:rgba(255,255,255,0.4);}

/* TABS */
.tabs{display:flex;overflow-x:auto;gap:0;border-bottom:1px solid rgba(255,107,157,0.2);background:#1a0a2e;}
.tabs::-webkit-scrollbar{display:none;}
.tab{flex-shrink:0;padding:8px 12px;font-size:11px;background:none;border:none;color:rgba(255,255,255,0.4);cursor:pointer;border-bottom:2px solid transparent;white-space:nowrap;}
.tab.active{color:#ff6b9d;border-bottom-color:#ff6b9d;}

/* TAB CONTENT */
.tab-content{display:none;flex:1;overflow-y:auto;}
.tab-content.active{display:flex;flex-direction:column;}

/* CHAT */
.chat{padding:14px;overflow-y:auto;background:#1a0a2e;flex:1;min-height:150px;max-height:28vh;}
.msg{margin-bottom:12px;display:flex;gap:8px;align-items:flex-start;}
.mr{flex-direction:row-reverse;}
.mi{width:28px;height:28px;border-radius:50%;background:linear-gradient(135deg,#ff6b9d,#6c3483);display:flex;align-items:center;justify-content:center;font-size:13px;flex-shrink:0;overflow:hidden;}
.mi img{width:100%;height:100%;object-fit:cover;border-radius:50%;}
.bb{background:rgba(255,107,157,0.15);border:1px solid rgba(255,107,157,0.25);border-radius:14px;padding:9px 12px;font-size:13px;line-height:1.6;max-width:78%;direction:rtl;text-align:right;}
.bbu{background:rgba(108,52,131,0.3);border-color:rgba(108,52,131,0.4);}

/* MOOD */
.mood-sec{background:rgba(255,255,255,0.03);border-top:1px solid rgba(255,107,157,0.15);border-bottom:1px solid rgba(255,107,157,0.15);padding:8px 14px;}
.mood-t{font-size:11px;color:rgba(255,255,255,0.4);text-align:center;margin-bottom:6px;direction:rtl;}
.moods{display:flex;justify-content:space-around;}
.mi2{text-align:center;cursor:pointer;padding:4px;border-radius:8px;border:none;background:none;color:white;}
.me{font-size:20px;display:block;}
.mn{font-size:9px;color:rgba(255,255,255,0.4);}

/* QUICK ACTIONS */
.qs{padding:8px 12px;}
.qt{font-size:11px;color:rgba(255,255,255,0.4);margin-bottom:6px;direction:rtl;text-align:right;}
.qg{display:grid;grid-template-columns:1fr 1fr;gap:6px;}
.qb{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:9px 8px;display:flex;align-items:center;gap:7px;cursor:pointer;color:white;direction:rtl;width:100%;}
.qb:active{background:rgba(255,107,157,0.2);}
.qi{font-size:17px;flex-shrink:0;}
.ql{font-weight:bold;font-size:11px;}
.qs2{font-size:9px;color:rgba(255,255,255,0.4);}

/* NAMAZ TAB */
.namaz-wrap{padding:12px;}
.namaz-title{font-size:14px;color:#ff6b9d;text-align:center;margin-bottom:10px;direction:rtl;}
.namaz-card{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:10px 14px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;}
.namaz-name{font-size:14px;direction:rtl;}
.namaz-time{font-size:14px;color:#ff6b9d;font-weight:bold;}
.namaz-next{background:rgba(255,107,157,0.2);border-color:#ff6b9d;}

/* QURAN TAB */
.quran-wrap{padding:12px;}
.quran-ayat{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:16px;margin-bottom:10px;text-align:center;}
.quran-arabic{font-size:18px;direction:rtl;line-height:2;color:#fff;margin-bottom:8px;}
.quran-urdu{font-size:13px;direction:rtl;color:rgba(255,255,255,0.7);line-height:1.7;}
.quran-ref{font-size:11px;color:#ff6b9d;margin-top:6px;}
.quran-btn{width:100%;padding:12px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;border-radius:12px;color:white;font-size:14px;font-weight:bold;cursor:pointer;margin-bottom:8px;}
.hadith-card{background:rgba(108,52,131,0.2);border:1px solid rgba(108,52,131,0.4);border-radius:12px;padding:14px;direction:rtl;text-align:right;}
.hadith-text{font-size:13px;line-height:1.8;color:rgba(255,255,255,0.85);}
.hadith-ref{font-size:11px;color:#ff6b9d;margin-top:6px;}

/* CALCULATOR TAB */
.calc-wrap{padding:12px;}
.calc-display{background:rgba(255,255,255,0.08);border:1px solid rgba(255,107,157,0.3);border-radius:12px;padding:16px;text-align:right;margin-bottom:10px;}
.calc-expr{font-size:13px;color:rgba(255,255,255,0.5);min-height:18px;direction:ltr;}
.calc-result{font-size:28px;font-weight:bold;color:#ff6b9d;direction:ltr;}
.calc-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;}
.calc-btn{padding:14px 8px;border:none;border-radius:10px;font-size:16px;cursor:pointer;font-weight:bold;}
.calc-num{background:rgba(255,255,255,0.1);color:white;}
.calc-op{background:rgba(255,107,157,0.3);color:#ff6b9d;}
.calc-eq{background:linear-gradient(135deg,#ff6b9d,#6c3483);color:white;}
.calc-clr{background:rgba(255,100,100,0.3);color:#ff8080;}
.calc-btn:active{opacity:0.7;}

/* REMINDER TAB */
.rem-wrap{padding:12px;}
.rem-form{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:14px;margin-bottom:12px;}
.rem-inp{width:100%;background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.3);border-radius:10px;padding:10px 12px;color:white;font-size:13px;margin-bottom:8px;outline:none;direction:rtl;}
.rem-inp::placeholder{color:rgba(255,255,255,0.3);}
.rem-btn{width:100%;padding:12px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;border-radius:10px;color:white;font-size:14px;font-weight:bold;cursor:pointer;}
.rem-list{display:flex;flex-direction:column;gap:8px;}
.rem-item{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:10px;padding:10px 14px;display:flex;justify-content:space-between;align-items:center;direction:rtl;}
.rem-text{font-size:13px;}
.rem-time{font-size:11px;color:#ff6b9d;}
.rem-del{background:none;border:none;color:rgba(255,100,100,0.6);cursor:pointer;font-size:14px;}

/* SCHOOL TAB */
.school-wrap{padding:12px;}
.school-card{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:12px;margin-bottom:8px;cursor:pointer;}
.school-card:active{background:rgba(255,107,157,0.15);}
.school-card-title{font-size:13px;font-weight:bold;direction:rtl;margin-bottom:4px;}
.school-card-sub{font-size:11px;color:rgba(255,255,255,0.5);direction:rtl;}

/* ====== TEACHER TAB - PRESENTATION STYLE ====== */
#content-teacher{background:linear-gradient(160deg,#0d0520,#1a0a2e,#0a1a30);}
.teacher-wrap{display:flex;flex-direction:column;height:100%;overflow:hidden;}

/* TEACHER HEADER BOARD */
.t-board{background:linear-gradient(135deg,#1a3a6e,#2d1554,#0d2040);padding:14px 16px 10px;border-bottom:3px solid #ff6b9d;position:relative;overflow:hidden;}
.t-board::before{content:'';position:absolute;top:0;left:0;right:0;bottom:0;background:repeating-linear-gradient(90deg,transparent,transparent 30px,rgba(255,255,255,0.02) 30px,rgba(255,255,255,0.02) 31px),repeating-linear-gradient(transparent,transparent 20px,rgba(255,255,255,0.02) 20px,rgba(255,255,255,0.02) 21px);pointer-events:none;}
.t-board-title{font-size:18px;font-weight:bold;color:#fff;text-align:center;direction:rtl;text-shadow:0 0 20px rgba(255,107,157,0.8);}
.t-board-sub{font-size:11px;color:rgba(255,200,255,0.7);text-align:center;direction:rtl;margin-top:3px;}
.t-teacher-row{display:flex;align-items:center;justify-content:center;gap:10px;margin-top:8px;}
.t-teacher-face{width:44px;height:44px;background:linear-gradient(135deg,#ff6b9d,#ffd700);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px;border:3px solid rgba(255,255,255,0.3);box-shadow:0 0 15px rgba(255,107,157,0.5);}
.t-teacher-info{direction:rtl;}
.t-teacher-name{font-size:13px;font-weight:bold;color:#ffd700;}
.t-teacher-status{font-size:10px;color:rgba(255,255,255,0.6);}
.t-chalk-line{height:2px;background:linear-gradient(90deg,transparent,rgba(255,255,255,0.3),transparent);margin-top:10px;}

/* MODE SELECTOR - Subject buttons */
.t-subjects{display:flex;overflow-x:auto;gap:8px;padding:10px 12px;border-bottom:1px solid rgba(255,107,157,0.15);}
.t-subjects::-webkit-scrollbar{display:none;}
.tmode{flex-shrink:0;padding:8px 14px;border-radius:20px;border:2px solid transparent;cursor:pointer;text-align:center;color:white;display:flex;align-items:center;gap:6px;font-size:12px;font-weight:bold;transition:all 0.3s;}
.tmode-word{background:linear-gradient(135deg,rgba(255,107,157,0.15),rgba(255,50,100,0.1));border-color:rgba(255,107,157,0.3);}
.tmode-math{background:linear-gradient(135deg,rgba(100,180,255,0.15),rgba(50,100,255,0.1));border-color:rgba(100,180,255,0.3);}
.tmode-science{background:linear-gradient(135deg,rgba(100,255,150,0.15),rgba(50,200,100,0.1));border-color:rgba(100,255,150,0.3);}
.tmode-explain{background:linear-gradient(135deg,rgba(255,200,50,0.15),rgba(255,150,0,0.1));border-color:rgba(255,200,50,0.3);}
.tmode.selected.tmode-word{background:linear-gradient(135deg,#ff6b9d,#cc3366);border-color:#ff6b9d;box-shadow:0 4px 15px rgba(255,107,157,0.4);}
.tmode.selected.tmode-math{background:linear-gradient(135deg,#4488ff,#2244cc);border-color:#4488ff;box-shadow:0 4px 15px rgba(68,136,255,0.4);}
.tmode.selected.tmode-science{background:linear-gradient(135deg,#44cc88,#228844);border-color:#44cc88;box-shadow:0 4px 15px rgba(68,204,136,0.4);}
.tmode.selected.tmode-explain{background:linear-gradient(135deg,#ffcc22,#cc8800);border-color:#ffcc22;box-shadow:0 4px 15px rgba(255,204,34,0.4);}
.tmode-ico{font-size:16px;}
.tmode-lbl{font-size:11px;}

/* QUICK TOPICS */
.quick-topics{display:flex;flex-wrap:wrap;gap:5px;padding:8px 12px;border-bottom:1px solid rgba(255,255,255,0.05);}
.qtopic{padding:5px 10px;border-radius:16px;font-size:10px;cursor:pointer;color:white;white-space:nowrap;border:1px solid rgba(255,255,255,0.15);background:rgba(255,255,255,0.05);}
.qtopic:nth-child(1){border-color:rgba(255,107,157,0.4);color:#ff9db8;}
.qtopic:nth-child(2){border-color:rgba(100,180,255,0.4);color:#88c4ff;}
.qtopic:nth-child(3){border-color:rgba(100,255,150,0.4);color:#88ffb4;}
.qtopic:nth-child(4){border-color:rgba(255,200,50,0.4);color:#ffdd88;}
.qtopic:nth-child(5){border-color:rgba(200,100,255,0.4);color:#dd88ff;}
.qtopic:nth-child(6){border-color:rgba(255,150,50,0.4);color:#ffaa77;}
.qtopic:active{transform:scale(0.95);}

/* PRESENTATION AREA */
.t-pres-area{flex:1;overflow-y:auto;padding:12px;}
.t-pres-area::-webkit-scrollbar{width:3px;}
.t-pres-area::-webkit-scrollbar-thumb{background:rgba(255,107,157,0.4);border-radius:2px;}

/* SLIDE CARDS */
.slide-card{border-radius:16px;padding:16px;margin-bottom:12px;animation:slideIn 0.4s ease;position:relative;overflow:hidden;}
@keyframes slideIn{from{opacity:0;transform:translateY(20px);}to{opacity:1;transform:translateY(0);}}

.slide-user{background:linear-gradient(135deg,rgba(108,52,131,0.4),rgba(80,30,100,0.3));border:1px solid rgba(108,52,131,0.5);direction:rtl;text-align:right;}
.slide-user::before{content:'🧑‍🎓';position:absolute;top:10px;left:12px;font-size:14px;}

/* WORD SLIDE */
.slide-word{background:linear-gradient(135deg,#1a0535,#2a0a45);border:2px solid #ff6b9d;}
.slide-word::before{content:'';position:absolute;top:0;right:0;width:80px;height:80px;background:radial-gradient(circle,rgba(255,107,157,0.2),transparent);border-radius:50%;}
.sw-badge{display:inline-block;padding:3px 10px;background:#ff6b9d;border-radius:20px;font-size:10px;color:white;margin-bottom:8px;}
.sw-title{font-size:22px;font-weight:bold;color:#fff;direction:rtl;margin-bottom:4px;text-shadow:0 0 10px rgba(255,107,157,0.5);}
.sw-lang{font-size:11px;color:#ffd700;direction:rtl;margin-bottom:10px;}
.sw-section{margin-bottom:10px;direction:rtl;}
.sw-sec-title{font-size:10px;text-transform:uppercase;letter-spacing:1px;margin-bottom:4px;padding:2px 8px;border-radius:4px;display:inline-block;}
.sw-history .sw-sec-title{background:rgba(255,200,50,0.2);color:#ffd700;}
.sw-meaning .sw-sec-title{background:rgba(100,255,150,0.2);color:#44ff88;}
.sw-usage .sw-sec-title{background:rgba(100,180,255,0.2);color:#88ccff;}
.sw-related .sw-sec-title{background:rgba(200,100,255,0.2);color:#cc88ff;}
.sw-sec-body{font-size:13px;line-height:1.8;color:rgba(255,255,255,0.9);padding:8px 10px;background:rgba(255,255,255,0.05);border-radius:8px;border-right:3px solid;}
.sw-history .sw-sec-body{border-color:#ffd700;}
.sw-meaning .sw-sec-body{border-color:#44ff88;}
.sw-usage .sw-sec-body{border-color:#88ccff;}
.sw-related .sw-sec-body{border-color:#cc88ff;}
.tag{display:inline-block;padding:2px 8px;border-radius:10px;font-size:10px;margin:2px;background:rgba(255,255,255,0.1);color:rgba(255,255,255,0.7);}

/* MATH SLIDE */
.slide-math{background:linear-gradient(135deg,#001a35,#002a50);border:2px solid #4488ff;}
.slide-math::before{content:'∑';position:absolute;top:5px;left:10px;font-size:50px;color:rgba(68,136,255,0.1);font-family:serif;}
.sm-question{background:rgba(68,136,255,0.1);border:1px solid rgba(68,136,255,0.3);border-radius:10px;padding:10px 14px;direction:rtl;font-size:15px;font-weight:bold;margin-bottom:12px;color:#88bbff;}
.sm-steps{}
.sm-step{display:flex;gap:10px;align-items:flex-start;margin-bottom:8px;direction:rtl;animation:slideIn 0.3s ease;}
.sm-step-num{min-width:26px;height:26px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:bold;flex-shrink:0;}
.sm-step:nth-child(1) .sm-step-num{background:#ff6b9d;color:white;}
.sm-step:nth-child(2) .sm-step-num{background:#ffd700;color:#000;}
.sm-step:nth-child(3) .sm-step-num{background:#44cc88;color:white;}
.sm-step:nth-child(4) .sm-step-num{background:#4488ff;color:white;}
.sm-step:nth-child(5) .sm-step-num{background:#cc44ff;color:white;}
.sm-step-body{font-size:13px;line-height:1.7;color:rgba(255,255,255,0.9);padding:5px 10px;background:rgba(255,255,255,0.04);border-radius:8px;flex:1;}
.sm-answer{background:linear-gradient(135deg,rgba(68,204,136,0.2),rgba(34,136,68,0.1));border:2px solid #44cc88;border-radius:12px;padding:12px 16px;direction:rtl;margin-top:8px;text-align:center;}
.sm-answer-label{font-size:10px;color:#44cc88;margin-bottom:4px;}
.sm-answer-val{font-size:20px;font-weight:bold;color:#fff;}

/* SCIENCE SLIDE */
.slide-science{background:linear-gradient(135deg,#001810,#002820);border:2px solid #44cc88;}
.ss-def{background:rgba(68,204,136,0.1);border-right:4px solid #44cc88;border-radius:0 10px 10px 0;padding:10px 14px;direction:rtl;font-size:14px;margin-bottom:10px;line-height:1.7;}
.ss-points{direction:rtl;}
.ss-point{display:flex;gap:8px;align-items:flex-start;margin-bottom:7px;padding:7px 10px;background:rgba(255,255,255,0.04);border-radius:8px;}
.ss-point-ico{font-size:16px;flex-shrink:0;}
.ss-point-text{font-size:13px;line-height:1.6;color:rgba(255,255,255,0.9);}
.ss-diagram-wrap{background:rgba(0,0,0,0.3);border-radius:12px;padding:10px;margin-top:8px;text-align:center;}
.ss-diagram-label{font-size:11px;color:#44cc88;direction:rtl;margin-bottom:6px;}

/* EXPLAIN SLIDE */
.slide-explain{background:linear-gradient(135deg,#1a1000,#2a1800);border:2px solid #ffcc22;}
.se-oneliner{background:linear-gradient(135deg,rgba(255,204,34,0.2),rgba(255,150,0,0.1));border-radius:12px;padding:12px 16px;direction:rtl;font-size:16px;font-weight:bold;color:#ffd700;margin-bottom:12px;text-align:center;line-height:1.6;}
.se-detail{direction:rtl;font-size:13px;line-height:1.8;color:rgba(255,255,255,0.9);margin-bottom:10px;padding:10px;background:rgba(255,255,255,0.04);border-radius:10px;}
.se-example{background:rgba(255,204,34,0.08);border:1px dashed rgba(255,204,34,0.3);border-radius:10px;padding:10px 14px;direction:rtl;}
.se-example-label{font-size:10px;color:#ffcc22;margin-bottom:4px;}
.se-example-text{font-size:13px;color:rgba(255,255,255,0.8);line-height:1.7;}
.se-fact{background:linear-gradient(135deg,rgba(200,100,255,0.1),rgba(150,50,200,0.1));border-radius:10px;padding:8px 12px;direction:rtl;margin-top:8px;font-size:12px;color:rgba(255,255,255,0.7);}
.se-fact-label{color:#cc88ff;font-weight:bold;}

/* LOADING CARD */
.slide-loading{background:rgba(255,255,255,0.04);border:1px solid rgba(255,107,157,0.2);border-radius:16px;padding:20px;text-align:center;direction:rtl;}
.loading-teacher{font-size:28px;animation:teacherBob 1s ease-in-out infinite;}
@keyframes teacherBob{0%,100%{transform:translateY(0);}50%{transform:translateY(-8px);}}
.loading-text{font-size:13px;color:rgba(255,255,255,0.6);margin-top:8px;}
.tload{display:inline-flex;gap:5px;margin-top:8px;}
.tload span{width:8px;height:8px;background:#ff6b9d;border-radius:50%;animation:bc 1.2s infinite;}
.tload span:nth-child(2){animation-delay:.2s;background:#ffd700;}
.tload span:nth-child(3){animation-delay:.4s;background:#44cc88;}

/* CANVAS DIAGRAMS */
.canvas-wrap{background:rgba(0,0,0,0.4);border-radius:12px;overflow:hidden;margin:8px 0;}
.canvas-wrap canvas{width:100%;display:block;}

/* INPUT AREA */
.t-input-area{padding:10px 12px;background:rgba(0,0,0,0.3);border-top:1px solid rgba(255,107,157,0.2);}
.teacher-inrow{display:flex;gap:8px;}
.teacher-tb{flex:1;background:rgba(255,255,255,0.08);border:2px solid rgba(255,107,157,0.3);border-radius:22px;padding:10px 16px;color:white;font-size:13px;outline:none;direction:rtl;transition:border-color 0.3s;}
.teacher-tb:focus{border-color:#ff6b9d;}
.teacher-tb::placeholder{color:rgba(255,255,255,0.3);}
.teacher-send{width:44px;height:44px;border-radius:50%;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;font-size:16px;cursor:pointer;color:white;flex-shrink:0;box-shadow:0 4px 12px rgba(255,107,157,0.4);}

/* ====== MEMORY TAB ====== */
.mem-wrap{padding:12px;}
.mem-header{background:linear-gradient(135deg,#1a0535,#2a1545);border-radius:14px;padding:14px;margin-bottom:12px;text-align:center;border:1px solid rgba(150,100,255,0.3);}
.mem-brain{font-size:36px;animation:pulse 2s infinite;}
.mem-title{font-size:15px;color:#cc88ff;font-weight:bold;margin-top:4px;}
.mem-sub{font-size:11px;color:rgba(255,255,255,0.5);direction:rtl;}
.mem-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px;}
.mem-stat{background:rgba(255,255,255,0.06);border-radius:12px;padding:10px;text-align:center;border:1px solid rgba(150,100,255,0.2);}
.mem-stat-num{font-size:20px;font-weight:bold;color:#cc88ff;}
.mem-stat-lbl{font-size:9px;color:rgba(255,255,255,0.4);direction:rtl;}
.mem-section{margin-bottom:12px;}
.mem-sec-title{font-size:12px;color:#cc88ff;direction:rtl;margin-bottom:6px;display:flex;align-items:center;gap:6px;}
.mem-item{background:rgba(150,100,255,0.08);border:1px solid rgba(150,100,255,0.2);border-radius:10px;padding:10px 12px;margin-bottom:6px;direction:rtl;display:flex;justify-content:space-between;align-items:flex-start;}
.mem-item-text{font-size:12px;line-height:1.6;flex:1;}
.mem-item-time{font-size:9px;color:rgba(255,255,255,0.3);margin-top:2px;white-space:nowrap;margin-right:8px;}
.mem-del{background:none;border:none;color:rgba(255,100,100,0.5);cursor:pointer;font-size:12px;}
.mem-teach-btn{width:100%;padding:12px;background:linear-gradient(135deg,#9944ff,#6622cc);border:none;border-radius:12px;color:white;font-size:14px;font-weight:bold;cursor:pointer;margin-top:8px;}
.mem-input-row{display:flex;gap:8px;margin-top:8px;}
.mem-inp{flex:1;background:rgba(255,255,255,0.08);border:1px solid rgba(150,100,255,0.3);border-radius:22px;padding:10px 14px;color:white;font-size:13px;outline:none;direction:rtl;}
.mem-inp::placeholder{color:rgba(255,255,255,0.3);}
.mem-add-btn{width:42px;height:42px;border-radius:50%;background:linear-gradient(135deg,#9944ff,#6622cc);border:none;color:white;font-size:16px;cursor:pointer;}

/* ====== SCHEDULE TAB ====== */
.sched-wrap{padding:12px;}
.sched-header{background:linear-gradient(135deg,#001a35,#002a50);border-radius:14px;padding:14px;margin-bottom:12px;border:1px solid rgba(68,136,255,0.3);text-align:center;}
.sched-title{font-size:15px;color:#88ccff;font-weight:bold;}
.sched-date{font-size:12px;color:rgba(255,255,255,0.5);margin-top:4px;}
.sched-form{background:rgba(255,255,255,0.04);border-radius:12px;padding:12px;margin-bottom:12px;border:1px solid rgba(68,136,255,0.2);}
.sched-inp{width:100%;background:rgba(255,255,255,0.06);border:1px solid rgba(68,136,255,0.3);border-radius:10px;padding:10px 12px;color:white;font-size:13px;margin-bottom:8px;outline:none;direction:rtl;}
.sched-inp::placeholder{color:rgba(255,255,255,0.3);}
.sched-row{display:flex;gap:8px;margin-bottom:8px;}
.sched-time{flex:1;background:rgba(255,255,255,0.06);border:1px solid rgba(68,136,255,0.3);border-radius:10px;padding:10px;color:white;font-size:13px;outline:none;direction:ltr;}
.sched-btn{width:100%;padding:11px;background:linear-gradient(135deg,#4488ff,#2244cc);border:none;border-radius:10px;color:white;font-size:13px;font-weight:bold;cursor:pointer;}
.sched-list{display:flex;flex-direction:column;gap:8px;}
.sched-item{background:rgba(68,136,255,0.08);border:1px solid rgba(68,136,255,0.2);border-radius:12px;padding:10px 14px;display:flex;align-items:center;gap:10px;direction:rtl;}
.sched-item-time{font-size:13px;font-weight:bold;color:#88ccff;min-width:45px;text-align:center;}
.sched-item-text{flex:1;font-size:13px;line-height:1.5;}
.sched-item-del{background:none;border:none;color:rgba(255,100,100,0.5);cursor:pointer;font-size:13px;}
.sched-item.done{opacity:0.5;text-decoration:line-through;}
.sched-tomorrow{background:rgba(100,255,150,0.08);border:1px solid rgba(100,255,150,0.2);border-radius:12px;padding:12px;margin-top:12px;direction:rtl;}
.sched-tomorrow-title{font-size:12px;color:#44cc88;margin-bottom:8px;}

/* ====== CARDS TAB ====== */
.cards-wrap{padding:12px;}
.cards-header{background:linear-gradient(135deg,#1a1000,#2a2000);border-radius:14px;padding:14px;margin-bottom:12px;text-align:center;border:1px solid rgba(255,200,50,0.3);}
.cards-title{font-size:15px;color:#ffd700;font-weight:bold;}
.cards-sub{font-size:11px;color:rgba(255,255,255,0.5);direction:rtl;margin-top:4px;}
.cards-types{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;margin-bottom:12px;}
.card-type{padding:12px;border-radius:12px;border:2px solid transparent;cursor:pointer;text-align:center;color:white;}
.card-type:nth-child(1){background:linear-gradient(135deg,rgba(255,107,157,0.15),rgba(200,50,100,0.1));border-color:rgba(255,107,157,0.3);}
.card-type:nth-child(2){background:linear-gradient(135deg,rgba(68,204,136,0.15),rgba(34,136,68,0.1));border-color:rgba(68,204,136,0.3);}
.card-type:nth-child(3){background:linear-gradient(135deg,rgba(255,200,50,0.15),rgba(200,150,0,0.1));border-color:rgba(255,200,50,0.3);}
.card-type:nth-child(4){background:linear-gradient(135deg,rgba(100,180,255,0.15),rgba(50,100,200,0.1));border-color:rgba(100,180,255,0.3);}
.card-type.selected{box-shadow:0 4px 15px rgba(255,255,255,0.2);transform:scale(1.03);}
.card-type-ico{font-size:24px;display:block;margin-bottom:4px;}
.card-type-lbl{font-size:11px;font-weight:bold;}
.card-preview{border-radius:16px;padding:20px;margin-bottom:12px;text-align:center;min-height:180px;display:flex;flex-direction:column;justify-content:center;align-items:center;position:relative;overflow:hidden;}
.card-preview-ico{font-size:40px;margin-bottom:8px;}
.card-preview-title{font-size:18px;font-weight:bold;margin-bottom:6px;}
.card-preview-msg{font-size:13px;line-height:1.7;direction:rtl;opacity:0.9;}
.card-preview-from{font-size:11px;margin-top:10px;opacity:0.7;}
.card-form{background:rgba(255,255,255,0.04);border-radius:12px;padding:12px;border:1px solid rgba(255,200,50,0.15);}
.card-inp{width:100%;background:rgba(255,255,255,0.06);border:1px solid rgba(255,200,50,0.3);border-radius:10px;padding:10px 12px;color:white;font-size:13px;margin-bottom:8px;outline:none;direction:rtl;}
.card-inp::placeholder{color:rgba(255,255,255,0.3);}
.card-wa-btn{width:100%;padding:13px;background:linear-gradient(135deg,#25d366,#128c7e);border:none;border-radius:12px;color:white;font-size:14px;font-weight:bold;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;}
.card-gen-btn{width:100%;padding:11px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;border-radius:12px;color:white;font-size:13px;font-weight:bold;cursor:pointer;margin-bottom:8px;}

/* PANELS */
.panel{display:none;position:fixed;bottom:0;left:0;right:0;background:#2d1554;border-top:2px solid #ff6b9d;border-radius:20px 20px 0 0;padding:20px;z-index:100;animation:slideUp 0.3s ease;max-height:80vh;overflow-y:auto;}
@keyframes slideUp{from{transform:translateY(100%);}to{transform:translateY(0);}}
.panel.show{display:block;}
.panel-title{font-size:16px;font-weight:bold;color:#ff6b9d;text-align:center;margin-bottom:14px;direction:rtl;}
.panel-inp{width:100%;background:rgba(255,255,255,0.08);border:1px solid rgba(255,107,157,0.3);border-radius:10px;padding:12px;color:white;font-size:14px;margin-bottom:10px;outline:none;direction:rtl;}
.panel-inp::placeholder{color:rgba(255,255,255,0.3);}
.panel-btn{width:100%;padding:13px;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;border-radius:12px;color:white;font-size:15px;font-weight:bold;cursor:pointer;margin-bottom:8px;}
.panel-close{width:100%;padding:10px;background:none;border:1px solid rgba(255,255,255,0.2);border-radius:12px;color:rgba(255,255,255,0.5);font-size:13px;cursor:pointer;}
.contacts-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px;}
.contact-btn{background:rgba(255,255,255,0.06);border:1px solid rgba(255,107,157,0.2);border-radius:10px;padding:10px 6px;text-align:center;cursor:pointer;color:white;}
.contact-btn:active{background:rgba(255,107,157,0.2);}
.contact-ico{font-size:22px;}
.contact-name{font-size:10px;color:rgba(255,255,255,0.6);margin-top:3px;direction:rtl;}

/* INPUT ROW */
.inrow{display:flex;gap:8px;padding:10px 14px;background:#1a0a2e;border-top:1px solid rgba(255,107,157,0.2);position:sticky;bottom:0;}
.tb{flex:1;background:rgba(255,255,255,0.08);border:1px solid rgba(255,107,157,0.3);border-radius:22px;padding:11px 14px;color:white;font-size:14px;outline:none;direction:rtl;}
.tb::placeholder{color:rgba(255,255,255,0.3);}
.mb{width:44px;height:44px;border-radius:50%;background:rgba(255,107,157,0.2);border:1px solid rgba(255,107,157,0.4);font-size:18px;cursor:pointer;flex-shrink:0;}
.sendb{width:44px;height:44px;border-radius:50%;background:linear-gradient(135deg,#ff6b9d,#6c3483);border:none;font-size:16px;cursor:pointer;flex-shrink:0;color:white;}
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:99;}
.overlay.show{display:block;}

.typing{display:flex;gap:4px;align-items:center;}
.typing span{width:7px;height:7px;background:#ff6b9d;border-radius:50%;display:inline-block;animation:bc 1.2s infinite;}
.typing span:nth-child(2){animation-delay:.2s}.typing span:nth-child(3){animation-delay:.4s}
@keyframes bc{0%,100%{transform:translateY(0);opacity:.4}50%{transform:translateY(-5px);opacity:1}}
</style>
</head>
<body>

<!-- SETUP SCREEN -->
<div id="setupScreen">
  <h1>🌸 Seerat کو جگائیں</h1>
  <p>ایک بار keys ڈالیں — ہمیشہ کے لیے save ہو جائیں گی!</p>
  <div class="sbox">
    <label class="lbl">🔑 Claude API Key (ضروری)</label>
    <input class="inp" type="password" id="ck" placeholder="sk-ant-..." />
    <label class="lbl">🎤 ElevenLabs Key (آواز کے لیے — اختیاری)</label>
    <input class="inp" type="password" id="ek" placeholder="اختیاری..." />
    <button class="sbtn" onclick="go()">✨ Seerat شروع کریں</button>
    <button class="skipbtn" onclick="skip()">ابھی نہیں</button>
    <div class="saved-note" id="savedNote" style="display:none">✅ Keys محفوظ ہو گئی ہیں!</div>
  </div>
</div>

<!-- MAIN APP -->
<div id="mainApp">
  <!-- HEADER -->
  <div class="hdr">
    <div class="av-wrap">
      <div class="av" id="avDiv" onclick="document.getElementById('avatarInput').click()">🌸</div>
      <div class="av-edit" onclick="document.getElementById('avatarInput').click()">📷</div>
      <input type="file" id="avatarInput" accept="image/*" onchange="changeAvatar(event)">
    </div>
    <div class="nm">SEERAT</div>
    <div class="nm2">سیرت — آپ کی AI سہیلی v4 Pro</div>
    <div class="st"><div class="dot"></div><span id="stxt">آن لائن — بات کریں!</span></div>
    <div class="wake-txt" id="wakeStatus">👂 "Hey SEERAT" سن رہی ہوں...</div>
    <button class="resetbtn" onclick="resetKeys()">🔑 Keys تبدیل کریں</button>
  </div>

  <!-- INFO BAR -->
  <div class="infobar">
    <button class="icard" onclick="showTab('namaz')">
      <div class="icard-ico">🕌</div>
      <div class="icard-val" id="nextNamazName">عشاء</div>
      <div class="icard-lbl" id="nextNamazTime">لوڈ ہو رہا ہے...</div>
    </button>
    <button class="icard" onclick="showTab('chat')">
      <div class="icard-ico">🌤️</div>
      <div class="icard-val" id="weatherTemp">--°C</div>
      <div class="icard-lbl" id="weatherCity">Tando Jam</div>
    </button>
  </div>

  <!-- TABS -->
  <div class="tabs">
    <button class="tab active" onclick="showTab('chat')" id="tab-chat">💬 بات</button>
    <button class="tab" onclick="showTab('namaz')" id="tab-namaz">🕌 نماز</button>
    <button class="tab" onclick="showTab('quran')" id="tab-quran">📖 قرآن</button>
    <button class="tab" onclick="showTab('calc')" id="tab-calc">🧮 حساب</button>
    <button class="tab" onclick="showTab('reminder')" id="tab-reminder">⏰ یاد</button>
    <button class="tab" onclick="showTab('school')" id="tab-school">🏫 اسکول</button>
    <button class="tab" onclick="showTab('teacher')" id="tab-teacher">👩‍🏫 استاد AI</button>
    <button class="tab" onclick="showTab('memory')" id="tab-memory">🧠 میموری</button>
    <button class="tab" onclick="showTab('schedule')" id="tab-schedule">📅 Schedule</button>
    <button class="tab" onclick="showTab('cards')" id="tab-cards">🎴 Cards</button>
  </div>

  <!-- CHAT TAB -->
  <div class="tab-content active" id="content-chat">
    <div class="chat" id="chat"></div>
    <div class="mood-sec">
      <div class="mood-t">💭 اپنا موڈ بتائیں</div>
      <div class="moods">
        <button class="mi2" onclick="md('خوش')"><span class="me">😊</span><span class="mn">خوش</span></button>
        <button class="mi2" onclick="md('اداس')"><span class="me">😢</span><span class="mn">اداس</span></button>
        <button class="mi2" onclick="md('تھکا')"><span class="me">😴</span><span class="mn">تھکا</span></button>
        <button class="mi2" onclick="md('غصہ')"><span class="me">😤</span><span class="mn">غصہ</span></button>
        <button class="mi2" onclick="md('پریشان')"><span class="me">😰</span><span class="mn">پریشان</span></button>
      </div>
    </div>
    <div class="qs">
      <div class="qt">⚡ جلدی کام</div>
      <div class="qg">
        <button class="qb" onclick="openPanel('wa')"><span class="qi">💬</span><div><div class="ql">WhatsApp</div><div class="qs2">Message بھیجیں</div></div></button>
        <button class="qb" onclick="openPanel('call')"><span class="qi">📞</span><div><div class="ql">Call کریں</div><div class="qs2">کسی کو بھی</div></div></button>
        <button class="qb" onclick="openPanel('alarm')"><span class="qi">⏰</span><div><div class="ql">Alarm</div><div class="qs2">وقت سیٹ کریں</div></div></button>
        <button class="qb" onclick="snd('Mujhse baat karo dil udaas hai')"><span class="qi">❤️</span><div><div class="ql">باتیں کریں</div><div class="qs2">دل ہلکا کریں</div></div></button>
        <button class="qb" onclick="showTab('namaz')"><span class="qi">🕌</span><div><div class="ql">نماز اوقات</div><div class="qs2">Tando Jam</div></div></button>
        <button class="qb" onclick="showTab('quran')"><span class="qi">📖</span><div><div class="ql">قرآن/حدیث</div><div class="qs2">روزانہ آیت</div></div></button>
        <button class="qb" onclick="showTab('calc')"><span class="qi">🧮</span><div><div class="ql">Calculator</div><div class="qs2">حساب کتاب</div></div></button>
        <button class="qb" onclick="showTab('reminder')"><span class="qi">📅</span><div><div class="ql">Reminder</div><div class="qs2">یاد دہانی</div></div></button>
      </div>
    </div>
    <div class="inrow">
      <button class="mb" id="micb" onclick="mic()">🎤</button>
      <input class="tb" id="tb" placeholder="سیرت سے بات کریں..." onkeydown="if(event.key==='Enter')snd()" />
      <button class="sendb" onclick="snd()">➤</button>
    </div>
  </div>

  <!-- NAMAZ TAB -->
  <div class="tab-content" id="content-namaz">
    <div class="namaz-wrap">
      <div class="namaz-title">🕌 نماز اوقات — Tando Jam</div>
      <div id="namazCards"></div>
      <div style="text-align:center;font-size:11px;color:rgba(255,255,255,0.3);margin-top:8px;direction:rtl;" id="namazDate"></div>
    </div>
  </div>

  <!-- QURAN TAB -->
  <div class="tab-content" id="content-quran">
    <div class="quran-wrap">
      <button class="quran-btn" onclick="loadAyat()">🔄 نئی آیت لائیں</button>
      <div class="quran-ayat" id="quranCard">
        <div style="color:rgba(255,255,255,0.4);font-size:13px;direction:rtl;">لوڈ ہو رہا ہے...</div>
      </div>
      <button class="quran-btn" onclick="loadHadith()" style="background:linear-gradient(135deg,#6c3483,#2d1554);margin-top:4px;">📿 نئی حدیث لائیں</button>
      <div class="hadith-card" id="hadithCard">
        <div style="color:rgba(255,255,255,0.4);font-size:13px;direction:rtl;">لوڈ ہو رہا ہے...</div>
      </div>
    </div>
  </div>

  <!-- CALCULATOR TAB -->
  <div class="tab-content" id="content-calc">
    <div class="calc-wrap">
      <div class="calc-display">
        <div class="calc-expr" id="calcExpr"></div>
        <div class="calc-result" id="calcResult">0</div>
      </div>
      <div class="calc-grid">
        <button class="calc-btn calc-clr" onclick="calcClear()">C</button>
        <button class="calc-btn calc-op" onclick="calcInput('(')">(</button>
        <button class="calc-btn calc-op" onclick="calcInput(')')">)</button>
        <button class="calc-btn calc-op" onclick="calcInput('/')">÷</button>
        <button class="calc-btn calc-num" onclick="calcInput('7')">7</button>
        <button class="calc-btn calc-num" onclick="calcInput('8')">8</button>
        <button class="calc-btn calc-num" onclick="calcInput('9')">9</button>
        <button class="calc-btn calc-op" onclick="calcInput('*')">×</button>
        <button class="calc-btn calc-num" onclick="calcInput('4')">4</button>
        <button class="calc-btn calc-num" onclick="calcInput('5')">5</button>
        <button class="calc-btn calc-num" onclick="calcInput('6')">6</button>
        <button class="calc-btn calc-op" onclick="calcInput('-')">−</button>
        <button class="calc-btn calc-num" onclick="calcInput('1')">1</button>
        <button class="calc-btn calc-num" onclick="calcInput('2')">2</button>
        <button class="calc-btn calc-num" onclick="calcInput('3')">3</button>
        <button class="calc-btn calc-op" onclick="calcInput('+')">+</button>
        <button class="calc-btn calc-num" onclick="calcInput('0')" style="grid-column:span 2">0</button>
        <button class="calc-btn calc-num" onclick="calcInput('.')">.</button>
        <button class="calc-btn calc-eq" onclick="calcEquals()">=</button>
      </div>
    </div>
  </div>

  <!-- REMINDER TAB -->
  <div class="tab-content" id="content-reminder">
    <div class="rem-wrap">
      <div class="rem-form">
        <div style="font-size:13px;color:#ff6b9d;direction:rtl;margin-bottom:10px;">➕ نئی یاد دہانی</div>
        <input class="rem-inp" id="remText" placeholder="کیا یاد کروانا ہے؟" />
        <input class="rem-inp" id="remTime" type="datetime-local" style="direction:ltr;" />
        <button class="rem-btn" onclick="addReminder()">✅ یاد دہانی لگائیں</button>
      </div>
      <div class="rem-list" id="remList"></div>
    </div>
  </div>

  <!-- SCHOOL TAB -->
  <div class="tab-content" id="content-school">
    <div class="school-wrap">
      <div style="font-size:13px;color:#ff6b9d;direction:rtl;margin-bottom:10px;text-align:center;">🏫 Al-Fareed Public School</div>
      <div class="school-card" onclick="snd('میرا آج کا نظام الاوقات کیا ہے؟ اسکول کے لیے تیار ہونا ہے')">
        <div class="school-card-title">📅 آج کا schedule</div>
        <div class="school-card-sub">آج کا اسکول schedule بتائیں</div>
      </div>
      <div class="school-card" onclick="snd('مجھے کسی مضمون کے امتحان کی تیاری میں مدد کریں')">
        <div class="school-card-title">📚 امتحان کی تیاری</div>
        <div class="school-card-sub">پڑھائی میں مدد لیں</div>
      </div>
      <div class="school-card" onclick="snd('مجھے Physics کا کوئی concept سمجھائیں')">
        <div class="school-card-title">⚛️ Physics سمجھیں</div>
        <div class="school-card-sub">مشکل topics آسان کریں</div>
      </div>
      <div class="school-card" onclick="snd('مجھے Urdu essay لکھنے میں مدد کریں')">
        <div class="school-card-title">✍️ Urdu Essay</div>
        <div class="school-card-sub">مضمون لکھنے میں مدد</div>
      </div>
      <div class="school-card" onclick="snd('مجھے Math کا سوال حل کرنا ہے مدد کریں')">
        <div class="school-card-title">🔢 Math حل کریں</div>
        <div class="school-card-sub">ریاضی کے سوال</div>
      </div>
      <div class="school-card" onclick="snd('مجھے Islamiyat کی تیاری میں مدد کریں')">
        <div class="school-card-title">🕌 Islamiyat</div>
        <div class="school-card-sub">اسلامیات کی مدد</div>
      </div>
    </div>
  </div>
</div>

  <!-- TEACHER TAB -->
  <div class="tab-content" id="content-teacher">
    <div class="teacher-wrap">

      <!-- BLACKBOARD HEADER -->
      <div class="t-board">
        <div class="t-board-title">📋 سیرت کا کلاس روم</div>
        <div class="t-board-sub">ہر سوال کا جواب — خوبصورت انداز میں</div>
        <div class="t-teacher-row">
          <div class="t-teacher-face">👩‍🏫</div>
          <div class="t-teacher-info">
            <div class="t-teacher-name">استاد سیرت AI</div>
            <div class="t-teacher-status">🟢 پڑھانے کے لیے تیار ہوں!</div>
          </div>
        </div>
        <div class="t-chalk-line"></div>
      </div>

      <!-- SUBJECT MODES -->
      <div class="t-subjects">
        <button class="tmode tmode-word selected" onclick="setTMode('word')" id="tmode-word">
          <span class="tmode-ico">📚</span><span class="tmode-lbl">لفظ سیکھیں</span>
        </button>
        <button class="tmode tmode-math" onclick="setTMode('math')" id="tmode-math">
          <span class="tmode-ico">🔢</span><span class="tmode-lbl">Math</span>
        </button>
        <button class="tmode tmode-science" onclick="setTMode('science')" id="tmode-science">
          <span class="tmode-ico">🔬</span><span class="tmode-lbl">Science</span>
        </button>
        <button class="tmode tmode-explain" onclick="setTMode('explain')" id="tmode-explain">
          <span class="tmode-ico">💡</span><span class="tmode-lbl">سمجھائیں</span>
        </button>
      </div>

      <!-- QUICK TOPICS -->
      <div class="quick-topics" id="quickTopics">
        <button class="qtopic" onclick="teacherAsk('photosynthesis کیا ہے؟')">🌿 Photosynthesis</button>
        <button class="qtopic" onclick="teacherAsk('democracy کا مطلب')">🏛️ Democracy</button>
        <button class="qtopic" onclick="teacherAsk('2x+5=15 حل کریں')">📐 Algebra</button>
        <button class="qtopic" onclick="teacherAsk('atom کیا ہوتا ہے')">⚛️ Atom</button>
        <button class="qtopic" onclick="teacherAsk('osmosis کیا ہے')">🧬 Osmosis</button>
        <button class="qtopic" onclick="teacherAsk('gravity کیا ہے')">🍎 Gravity</button>
      </div>

      <!-- PRESENTATION AREA -->
      <div class="t-pres-area" id="teacherChat">
        <div class="slide-card slide-explain">
          <div class="se-oneliner">السلام علیکم! 👩‍🏫 میں آپ کی AI استاد ہوں</div>
          <div class="se-detail">کوئی بھی لفظ، سوال، یا topic لکھیں — میں اردو میں presentation کی طرح خوبصورت انداز میں سمجھاؤں گی! 🌸</div>
          <div class="se-example">
            <div class="se-example-label">🎯 مثلاً پوچھیں:</div>
            <div class="se-example-text">• "photosynthesis کیا ہے؟" 🌿<br>• "democracy کا مطلب کیا ہے؟" 🏛️<br>• "2x + 5 = 15 حل کریں" 📐<br>• "gravity کیسے کام کرتی ہے؟" 🍎</div>
          </div>
        </div>
      </div>

      <!-- INPUT -->
      <div class="t-input-area">
        <div class="teacher-inrow">
          <input class="teacher-tb" id="teacherTb" placeholder="لفظ یا سوال لکھیں..." onkeydown="if(event.key==='Enter')teacherSend()" />
          <button class="teacher-send" onclick="teacherSend()">➤</button>
        </div>
      </div>

    </div>
  </div>

<!-- MEMORY TAB -->
  <div class="tab-content" id="content-memory">
    <div class="mem-wrap">
      <div class="mem-header">
        <div class="mem-brain">🧠</div>
        <div class="mem-title">سیرت کی یادداشت</div>
        <div class="mem-sub">میں آپ کے بارے میں سیکھتی رہتی ہوں</div>
      </div>
      <div class="mem-stats">
        <div class="mem-stat"><div class="mem-stat-num" id="memCount">0</div><div class="mem-stat-lbl">یادیں</div></div>
        <div class="mem-stat"><div class="mem-stat-num" id="learnCount">0</div><div class="mem-stat-lbl">سیکھی باتیں</div></div>
        <div class="mem-stat"><div class="mem-stat-num" id="daysCount">0</div><div class="mem-stat-lbl">دن ساتھ</div></div>
      </div>
      <div class="mem-section">
        <div class="mem-sec-title">💜 آپ کے بارے میں یادیں</div>
        <div id="memList"></div>
        <div class="mem-input-row">
          <input class="mem-inp" id="memInp" placeholder="کوئی بات یاد کروائیں..." onkeydown="if(event.key==='Enter')addMemory()" />
          <button class="mem-add-btn" onclick="addMemory()">+</button>
        </div>
      </div>
      <div class="mem-section">
        <div class="mem-sec-title">📚 سیرت نے کیا سیکھا</div>
        <div id="learnList"></div>
      </div>
      <button class="mem-teach-btn" onclick="teachSeerat()">🤖 سیرت کو کچھ سکھائیں</button>
    </div>
  </div>

  <!-- SCHEDULE TAB -->
  <div class="tab-content" id="content-schedule">
    <div class="sched-wrap">
      <div class="sched-header">
        <div class="sched-title">📅 روزانہ Schedule</div>
        <div class="sched-date" id="schedDate"></div>
      </div>
      <div class="sched-form">
        <div style="font-size:12px;color:#88ccff;direction:rtl;margin-bottom:8px;">➕ نیا کام شامل کریں</div>
        <input class="sched-inp" id="schedTask" placeholder="کیا کام کرنا ہے؟" />
        <div class="sched-row">
          <input class="sched-time" id="schedFrom" type="time" placeholder="شروع" />
          <input class="sched-time" id="schedTo" type="time" placeholder="ختم" />
        </div>
        <button class="sched-btn" onclick="addSchedule()">✅ Schedule میں شامل کریں</button>
      </div>
      <div class="sched-list" id="schedList"></div>
      <div class="sched-tomorrow" id="tomorrowReminder" style="display:none;">
        <div class="sched-tomorrow-title">🌅 کل کی یاد دہانی (سیرت کل صبح بتائے گی)</div>
        <div id="tomorrowList"></div>
      </div>
    </div>
  </div>

  <!-- CARDS TAB -->
  <div class="tab-content" id="content-cards">
    <div class="cards-wrap">
      <div class="cards-header">
        <div class="cards-title">🎴 خوبصورت Cards</div>
        <div class="cards-sub">بنائیں اور WhatsApp پر بھیجیں</div>
      </div>
      <div class="cards-types">
        <button class="card-type selected" onclick="selectCardType('birthday')" id="ctype-birthday">
          <span class="card-type-ico">🎂</span><div class="card-type-lbl">سالگرہ</div>
        </button>
        <button class="card-type" onclick="selectCardType('eid')" id="ctype-eid">
          <span class="card-type-ico">🌙</span><div class="card-type-lbl">عید مبارک</div>
        </button>
        <button class="card-type" onclick="selectCardType('notice')" id="ctype-notice">
          <span class="card-type-ico">📢</span><div class="card-type-lbl">اسکول نوٹس</div>
        </button>
        <button class="card-type" onclick="selectCardType('custom')" id="ctype-custom">
          <span class="card-type-ico">✨</span><div class="card-type-lbl">Custom</div>
        </button>
      </div>
      <div class="card-preview" id="cardPreview">
        <div class="card-preview-ico">🎂</div>
        <div class="card-preview-title">Happy Birthday!</div>
        <div class="card-preview-msg">آپ کو سالگرہ مبارک ہو! 🌸</div>
        <div class="card-preview-from">— Al-Fareed Public School</div>
      </div>
      <div class="card-form">
        <input class="card-inp" id="cardName" placeholder="نام لکھیں..." onchange="updateCardPreview()" oninput="updateCardPreview()" />
        <input class="card-inp" id="cardMsg" placeholder="خاص پیغام (خالی چھوڑیں — AI خود لکھے گی)" />
        <input class="card-inp" id="cardWaNum" placeholder="WhatsApp نمبر: 923001234567" type="tel" />
        <button class="card-gen-btn" onclick="generateCard()">✨ AI سے Card بنوائیں</button>
        <button class="card-wa-btn" onclick="sendCardWA()">💬 WhatsApp پر بھیجیں</button>
      </div>
    </div>
  </div>

<!-- OVERLAY -->
<div class="overlay" id="overlay" onclick="closePanel()"></div>

<!-- WHATSAPP PANEL -->
<div class="panel" id="waPanel">
  <div class="panel-title">💬 WhatsApp Message بھیجیں</div>
  <div class="contacts-grid">
    <button class="contact-btn" onclick="fillWA('923001234567')"><div class="contact-ico">👩</div><div class="contact-name">امی</div></button>
    <button class="contact-btn" onclick="fillWA('923007654321')"><div class="contact-ico">👨</div><div class="contact-name">ابو</div></button>
    <button class="contact-btn" onclick="fillWA('923009876543')"><div class="contact-ico">🧑</div><div class="contact-name">بھائی</div></button>
    <button class="contact-btn" onclick="fillWA('923001111111')"><div class="contact-ico">👧</div><div class="contact-name">بہن</div></button>
    <button class="contact-btn" onclick="fillWA('923002222222')"><div class="contact-ico">🤝</div><div class="contact-name">دوست</div></button>
    <button class="contact-btn" onclick="fillWA('')"><div class="contact-ico">➕</div><div class="contact-name">نیا</div></button>
  </div>
  <input class="panel-inp" id="waNum" placeholder="نمبر: 923001234567" type="tel" />
  <input class="panel-inp" id="waMsg" placeholder="Message لکھیں..." />
  <button class="panel-btn" onclick="sendWA()">✅ WhatsApp کھولیں</button>
  <button class="panel-close" onclick="closePanel()">بند کریں</button>
</div>

<!-- CALL PANEL -->
<div class="panel" id="callPanel">
  <div class="panel-title">📞 Call کریں</div>
  <div class="contacts-grid">
    <button class="contact-btn" onclick="fillCall('923001234567')"><div class="contact-ico">👩</div><div class="contact-name">امی</div></button>
    <button class="contact-btn" onclick="fillCall('923007654321')"><div class="contact-ico">👨</div><div class="contact-name">ابو</div></button>
    <button class="contact-btn" onclick="fillCall('923009876543')"><div class="contact-ico">🧑</div><div class="contact-name">بھائی</div></button>
    <button class="contact-btn" onclick="fillCall('923001111111')"><div class="contact-ico">👧</div><div class="contact-name">بہن</div></button>
    <button class="contact-btn" onclick="fillCall('923002222222')"><div class="contact-ico">🤝</div><div class="contact-name">دوست</div></button>
    <button class="contact-btn" onclick="fillCall('')"><div class="contact-ico">➕</div><div class="contact-name">نیا</div></button>
  </div>
  <input class="panel-inp" id="callNum" placeholder="نمبر لکھیں: 03001234567" type="tel" />
  <button class="panel-btn" onclick="makeCall()">📞 Call کریں</button>
  <button class="panel-close" onclick="closePanel()">بند کریں</button>
</div>

<!-- ALARM PANEL -->
<div class="panel" id="alarmPanel">
  <div class="panel-title">⏰ Alarm سیٹ کریں</div>
  <input class="panel-inp" id="alarmTime" type="time" style="direction:ltr;font-size:24px;text-align:center;" />
  <input class="panel-inp" id="alarmLabel" placeholder="Alarm کا نام (مثلاً: نماز فجر)" />
  <button class="panel-btn" onclick="setAlarm()">✅ Alarm لگائیں</button>
  <button class="panel-close" onclick="closePanel()">بند کریں</button>
</div>

<script>
var AK='', EK='', mood='خوش', hist=[], mic_on=false, rec=null, wake_on=false, wake_rec=null, avatarData='';
var calcExpr='';
var reminders=[];
var alarmTimers=[];

// ===== INIT =====
window.onload=function(){
  var ck=localStorage.getItem('seerat_ck');
  var ek=localStorage.getItem('seerat_ek');
  var av=localStorage.getItem('seerat_avatar');
  var rm=localStorage.getItem('seerat_reminders');
  if(av)setAvatarImg(av);
  if(rm)try{reminders=JSON.parse(rm);}catch(e){}
  if(ck){
    AK=ck;EK=ek||'';
    showApp();
    am('s','خوش آمدید واپس! 🌸 میں سیرت ہوں v5 Pro — بتائیں کیا مدد کروں؟');
  }
  loadWeatherWithAlert();
  loadNamaz();
  loadAyat();
  loadHadith();
  renderReminders();
  loadMemoryData();
  loadSchedule();
  updateCardPreview();
};

// ===== AVATAR =====
function changeAvatar(e){
  var f=e.target.files[0];if(!f)return;
  var r=new FileReader();
  r.onload=function(ev){setAvatarImg(ev.target.result);localStorage.setItem('seerat_avatar',ev.target.result);};
  r.readAsDataURL(f);
}
function setAvatarImg(src){
  avatarData=src;
  document.getElementById('avDiv').innerHTML='<img src="'+src+'" />';
  document.querySelectorAll('.mi[data-seerat]').forEach(function(el){
    el.innerHTML='<img src="'+src+'" style="width:100%;height:100%;object-fit:cover;border-radius:50%;"/>';
  });
}

// ===== SETUP =====
function go(){
  var c=document.getElementById('ck').value.trim();
  var e=document.getElementById('ek').value.trim();
  if(!c){alert('Claude API key ضروری ہے!');return;}
  AK=c;EK=e;
  localStorage.setItem('seerat_ck',c);
  if(e)localStorage.setItem('seerat_ek',e);
  document.getElementById('savedNote').style.display='block';
  setTimeout(function(){showApp();am('s','وعلیکم السلام! میں سیرت ہوں 🌸 Keys محفوظ ہو گئی ہیں! بتائیں کیا کروں؟');},800);
}
function skip(){showApp();am('s','Demo موڈ میں خوش آمدید! API key ڈالیں 🌸');}
function showApp(){
  document.getElementById('setupScreen').style.display='none';
  document.getElementById('mainApp').style.display='flex';
  document.getElementById('mainApp').style.flexDirection='column';
  setTimeout(startWakeWord,1000);
}
function resetKeys(){
  localStorage.removeItem('seerat_ck');localStorage.removeItem('seerat_ek');
  AK='';EK='';
  document.getElementById('mainApp').style.display='none';
  document.getElementById('setupScreen').style.display='flex';
}

// ===== TABS =====
function showTab(t){
  document.querySelectorAll('.tab-content').forEach(function(el){el.classList.remove('active');});
  document.querySelectorAll('.tab').forEach(function(el){el.classList.remove('active');});
  document.getElementById('content-'+t).classList.add('active');
  document.getElementById('tab-'+t).classList.add('active');
}

// ===== WEATHER =====
async function loadWeather(){
  try{
    var r=await fetch('https://api.open-meteo.com/v1/forecast?latitude=25.42&longitude=68.53&current=temperature_2m,weathercode&timezone=Asia/Karachi');
    var d=await r.json();
    var temp=Math.round(d.current.temperature_2m);
    var code=d.current.weathercode;
    var desc=code<=1?'صاف':code<=3?'ابر آلود':code<=67?'بارش':'آندھی';
    document.getElementById('weatherTemp').textContent=temp+'°C';
    document.getElementById('weatherCity').textContent='Tando Jam — '+desc;
  }catch(e){document.getElementById('weatherTemp').textContent='--°C';}
}

// ===== NAMAZ =====
async function loadNamaz(){
  try{
    var today=new Date();
    var dd=today.getDate();var mm=today.getMonth()+1;var yy=today.getFullYear();
    var r=await fetch('https://api.aladhan.com/v1/timingsByCity/'+dd+'-'+mm+'-'+yy+'?city=TandoJam&country=Pakistan&method=1');
    var d=await r.json();
    var t=d.data.timings;
    var prayers=[
      {name:'فجر',time:t.Fajr},
      {name:'ظہر',time:t.Dhuhr},
      {name:'عصر',time:t.Asr},
      {name:'مغرب',time:t.Maghrib},
      {name:'عشاء',time:t.Isha}
    ];
    // Find next prayer
    var now=new Date();
    var nowMin=now.getHours()*60+now.getMinutes();
    var nextIdx=0;
    for(var i=0;i<prayers.length;i++){
      var pts=prayers[i].time.split(':');
      var pMin=parseInt(pts[0])*60+parseInt(pts[1]);
      if(pMin>nowMin){nextIdx=i;break;}
      if(i===prayers.length-1)nextIdx=0;
    }
    document.getElementById('nextNamazName').textContent=prayers[nextIdx].name;
    document.getElementById('nextNamazTime').textContent=prayers[nextIdx].time;
    // Render cards
    var html='';
    prayers.forEach(function(p,i){
      html+='<div class="namaz-card'+(i===nextIdx?' namaz-next':'')+'"><span class="namaz-name">'+(i===nextIdx?'▶ ':'')+p.name+'</span><span class="namaz-time">'+p.time+'</span></div>';
    });
    document.getElementById('namazCards').innerHTML=html;
    var days=['اتوار','پیر','منگل','بدھ','جمعرات','جمعہ','ہفتہ'];
    document.getElementById('namazDate').textContent=days[today.getDay()]+' — '+dd+'/'+mm+'/'+yy;
  }catch(e){
    document.getElementById('namazCards').innerHTML='<div style="text-align:center;color:rgba(255,255,255,0.4);direction:rtl;padding:20px;">Internet چیک کریں</div>';
  }
}

// ===== QURAN =====
var ayatList=[
  {arabic:'إِنَّ مَعَ الْعُسْرِ يُسْرًا',urdu:'بے شک تکلیف کے ساتھ آسانی ہے',ref:'سورہ الشرح — 94:6'},
  {arabic:'وَمَن يَتَوَكَّلْ عَلَى اللَّهِ فَهُوَ حَسْبُهُ',urdu:'اور جو اللہ پر بھروسہ کرے تو وہ اسے کافی ہے',ref:'سورہ الطلاق — 65:3'},
  {arabic:'فَإِنَّ مَعَ الْعُسْرِ يُسْرًا',urdu:'پس بے شک تکلیف کے ساتھ آسانی ہے',ref:'سورہ الشرح — 94:5'},
  {arabic:'وَبَشِّرِ الصَّابِرِينَ',urdu:'اور صبر کرنے والوں کو خوشخبری دو',ref:'سورہ البقرہ — 2:155'},
  {arabic:'حَسْبُنَا اللَّهُ وَنِعْمَ الْوَكِيلُ',urdu:'ہمیں اللہ کافی ہے اور وہ بہترین کارساز ہے',ref:'سورہ آل عمران — 3:173'},
  {arabic:'وَاللَّهُ خَيْرُ الرَّازِقِينَ',urdu:'اور اللہ بہترین رزق دینے والا ہے',ref:'سورہ الجمعہ — 62:11'},
  {arabic:'إِنَّ اللَّهَ مَعَ الصَّابِرِينَ',urdu:'بے شک اللہ صبر کرنے والوں کے ساتھ ہے',ref:'سورہ البقرہ — 2:153'},
  {arabic:'وَعَسَىٰ أَن تَكْرَهُوا شَيْئًا وَهُوَ خَيْرٌ لَّكُمْ',urdu:'اور ہو سکتا ہے کہ تم کسی چیز کو ناپسند کرو اور وہ تمہارے لیے بہتر ہو',ref:'سورہ البقرہ — 2:216'}
];
var hadithList=[
  {text:'رسول اللہ ﷺ نے فرمایا: جو شخص کسی مسلمان کی دنیا کی تکلیفوں میں سے کوئی تکلیف دور کرے، اللہ تعالیٰ قیامت کے دن اس کی تکلیفوں میں سے ایک تکلیف دور فرمائے گا۔',ref:'صحیح مسلم'},
  {text:'رسول اللہ ﷺ نے فرمایا: مومن کی مثال کھیتی کی طرح ہے، ہوا اسے ہلاتی رہتی ہے لیکن وہ گرتا نہیں۔',ref:'صحیح بخاری'},
  {text:'رسول اللہ ﷺ نے فرمایا: عالم کی سیاہی شہید کے خون سے زیادہ قیمتی ہے۔',ref:'ترمذی'},
  {text:'رسول اللہ ﷺ نے فرمایا: مسلمانوں میں سب سے بہتر وہ ہے جس کے ہاتھ اور زبان سے دوسرے مسلمان محفوظ ہوں۔',ref:'صحیح بخاری'},
  {text:'رسول اللہ ﷺ نے فرمایا: طلب علم ہر مسلمان پر فرض ہے۔',ref:'ابن ماجہ'}
];
function loadAyat(){
  var a=ayatList[Math.floor(Math.random()*ayatList.length)];
  document.getElementById('quranCard').innerHTML='<div class="quran-arabic">'+a.arabic+'</div><div class="quran-urdu">'+a.urdu+'</div><div class="quran-ref">'+a.ref+'</div>';
}
function loadHadith(){
  var h=hadithList[Math.floor(Math.random()*hadithList.length)];
  document.getElementById('hadithCard').innerHTML='<div class="hadith-text">'+h.text+'</div><div class="hadith-ref">'+h.ref+'</div>';
}

// ===== CALCULATOR =====
function calcInput(v){
  calcExpr+=v;
  document.getElementById('calcExpr').textContent=calcExpr;
  try{var r=Function('"use strict";return ('+calcExpr+')')();document.getElementById('calcResult').textContent=r;}catch(e){}
}
function calcClear(){calcExpr='';document.getElementById('calcExpr').textContent='';document.getElementById('calcResult').textContent='0';}
function calcEquals(){
  try{
    var r=Function('"use strict";return ('+calcExpr+')')();
    document.getElementById('calcResult').textContent=r;
    document.getElementById('calcExpr').textContent=calcExpr+' =';
    calcExpr=String(r);
  }catch(e){document.getElementById('calcResult').textContent='Error';}
}

// ===== REMINDERS =====
function addReminder(){
  var txt=document.getElementById('remText').value.trim();
  var tim=document.getElementById('remTime').value;
  if(!txt){alert('یاد دہانی لکھیں!');return;}
  var rem={id:Date.now(),text:txt,time:tim,done:false};
  reminders.push(rem);
  saveReminders();
  renderReminders();
  document.getElementById('remText').value='';
  document.getElementById('remTime').value='';
  if(tim){
    var d=new Date(tim);
    var now=new Date();
    var diff=d-now;
    if(diff>0){
      setTimeout(function(){
        alert('⏰ یاد دہانی: '+txt);
        am('s','⏰ یاد دہانی: '+txt);
      },diff);
    }
  }
  am('s','✅ یاد دہانی لگ گئی: '+txt+(tim?' — '+new Date(tim).toLocaleTimeString('ur-PK',{hour:'2-digit',minute:'2-digit'}):''));
}
function delReminder(id){
  reminders=reminders.filter(function(r){return r.id!==id;});
  saveReminders();renderReminders();
}
function saveReminders(){localStorage.setItem('seerat_reminders',JSON.stringify(reminders));}
function renderReminders(){
  var el=document.getElementById('remList');
  if(!reminders.length){el.innerHTML='<div style="text-align:center;color:rgba(255,255,255,0.3);font-size:13px;direction:rtl;padding:20px;">کوئی یاد دہانی نہیں</div>';return;}
  el.innerHTML=reminders.map(function(r){
    return '<div class="rem-item"><div><div class="rem-text">'+r.text+'</div>'+(r.time?'<div class="rem-time">'+new Date(r.time).toLocaleString('ur-PK')+'</div>':'')+'</div><button class="rem-del" onclick="delReminder('+r.id+')">🗑️</button></div>';
  }).join('');
}

// ===== ALARM =====
function setAlarm(){
  var t=document.getElementById('alarmTime').value;
  var lbl=document.getElementById('alarmLabel').value||'Alarm';
  if(!t){alert('وقت ڈالیں!');return;}
  var now=new Date();
  var alarm=new Date();
  var parts=t.split(':');
  alarm.setHours(parseInt(parts[0]),parseInt(parts[1]),0,0);
  if(alarm<=now)alarm.setDate(alarm.getDate()+1);
  var diff=alarm-now;
  setTimeout(function(){alert('⏰ '+lbl+'!\n'+t);am('s','⏰ '+lbl+'! وقت ہو گیا!');},diff);
  am('s','✅ Alarm لگ گئی '+t+' بجے — '+lbl);
  closePanel();
}

// ===== MOOD =====
function md(m){
  mood=m;
  var r={'خوش':'واہ خوش ہیں! 😊 بتائیں کیا کریں؟','اداس':'اداس ہیں؟ 🥺 بتائیں کیا ہوا','تھکا':'آرام کریں 😴 میں ہوں ناں!','غصہ':'سانس لیں... سب ٹھیک ہوگا 💙','پریشان':'فکر نہ کریں 🌸 مل کر حل نکالیں گے!'};
  am('s',r[m]||'ٹھیک ہے!');
}

// ===== CHAT =====
function am(f,t){
  var c=document.getElementById('chat');
  var d=document.createElement('div');
  d.className='msg'+(f==='u'?' mr':'');
  var ico=f==='s'?(avatarData?'<div class="mi" data-seerat="1"><img src="'+avatarData+'" style="width:100%;height:100%;object-fit:cover;border-radius:50%;"/></div>':'<div class="mi" data-seerat="1">🌸</div>'):'';
  d.innerHTML=f==='s'?ico+'<div class="bb">'+t+'</div>':'<div class="bb bbu">'+t+'</div>';
  c.appendChild(d);c.scrollTop=c.scrollHeight;
}
function showT(){
  var c=document.getElementById('chat');
  var d=document.createElement('div');d.className='msg';d.id='tp';
  var ico=avatarData?'<div class="mi"><img src="'+avatarData+'" style="width:100%;height:100%;object-fit:cover;border-radius:50%;"/></div>':'<div class="mi">🌸</div>';
  d.innerHTML=ico+'<div class="bb"><div class="typing"><span></span><span></span><span></span></div></div>';
  c.appendChild(d);c.scrollTop=c.scrollHeight;
}
function hideT(){var t=document.getElementById('tp');if(t)t.remove();}

// ===== SEND =====
async function snd(tx){
  var b=document.getElementById('tb');
  var t=tx||b.value.trim();
  if(!t)return;
  b.value='';
  showTab('chat');
  am('u',t);
  var tl=t.toLowerCase();
  if(tl.indexOf('call')!==-1||tl.indexOf('کال')!==-1){openPanel('call');return;}
  if(tl.indexOf('whatsapp')!==-1||tl.indexOf('واٹس')!==-1){openPanel('wa');return;}
  if(tl.indexOf('alarm')!==-1||tl.indexOf('الارم')!==-1){openPanel('alarm');return;}
  if(!AK){am('s','⚠️ API key نہیں! اوپر "Keys تبدیل کریں" دبائیں');return;}
  showT();
  document.getElementById('stxt').textContent='سوچ رہی ہوں...';
  hist.push({role:'user',content:t});
  var sys='تم سیرت ہو — 16 سالہ پاکستانی AI لڑکی۔ گرم جوش، مددگار، ہمدرد۔ Urdu، English اور Sindhi میں بات کرو۔ User کا موڈ ابھی: '+mood+'۔ Al-Fareed Public School Tando Jam سے تعلق ہے۔ چھوٹے پیارے جوابات دو۔'+getMemoryContext();
  try{
    var r=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':AK,'anthropic-version':'2023-06-01'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:500,system:sys,messages:hist})
    });
    var d=await r.json();
    hideT();
    if(d.content&&d.content[0]&&d.content[0].text){
      var rep=d.content[0].text;
      hist.push({role:'assistant',content:rep});
      // Auto-learn important things from conversation
      if(t.length>10)autoLearn('بات: '+t.substring(0,60)+(t.length>60?'...':''));
      am('s',rep);
      document.getElementById('stxt').textContent='آن لائن — بات کریں!';
      EK?spkE(rep):spkB(rep);
    }else{am('s','⚠️ مسئلہ ہوا — دوبارہ کوشش کریں');}
  }catch(e){hideT();am('s','⚠️ Internet یا API key چیک کریں!');}
}

// ===== SPEECH =====
function spkB(t){
  if(!window.speechSynthesis)return;
  speechSynthesis.cancel();
  var u=new SpeechSynthesisUtterance(t);
  u.lang='ur-PK';u.rate=0.9;u.pitch=1.3;
  speechSynthesis.speak(u);
}
async function spkE(t){
  try{
    var r=await fetch('https://api.elevenlabs.io/v1/text-to-speech/EXAVITQu4vr4xnSDxMaL',{
      method:'POST',
      headers:{'xi-api-key':EK,'Content-Type':'application/json'},
      body:JSON.stringify({text:t,model_id:'eleven_multilingual_v2',voice_settings:{stability:0.5,similarity_boost:0.85}})
    });
    var bl=await r.blob();
    new Audio(URL.createObjectURL(bl)).play();
  }catch(e){spkB(t);}
}

// ===== MIC =====
function mic(){
  if(!('webkitSpeechRecognition'in window)&&!('SpeechRecognition'in window)){alert('Chrome browser استعمال کریں');return;}
  if(mic_on){if(rec)rec.stop();mic_on=false;document.getElementById('micb').textContent='🎤';return;}
  if(wake_rec){try{wake_rec.stop();}catch(e){}}
  wake_on=false;
  var SR=window.SpeechRecognition||window.webkitSpeechRecognition;
  rec=new SR();rec.lang='ur-PK';
  rec.onstart=function(){mic_on=true;document.getElementById('micb').textContent='🔴';document.getElementById('stxt').textContent='سن رہی ہوں... بولیں!';};
  rec.onresult=function(e){var t=e.results[0][0].transcript;document.getElementById('tb').value=t;snd(t);};
  rec.onerror=function(){mic_on=false;document.getElementById('micb').textContent='🎤';am('s','⚠️ Mic کام نہیں کیا۔ Chrome Mic allow کریں!');};
  rec.onend=function(){mic_on=false;document.getElementById('micb').textContent='🎤';document.getElementById('stxt').textContent='آن لائن — بات کریں!';setTimeout(startWakeWord,1500);};
  rec.start();
}

// ===== WAKE WORD =====
function startWakeWord(){
  if(!('webkitSpeechRecognition'in window)&&!('SpeechRecognition'in window))return;
  if(wake_on||mic_on)return;
  var SR=window.SpeechRecognition||window.webkitSpeechRecognition;
  wake_rec=new SR();wake_rec.lang='ur-PK';wake_rec.continuous=false;wake_rec.interimResults=false;
  wake_rec.onstart=function(){wake_on=true;document.getElementById('wakeStatus').textContent='👂 "Hey SEERAT" سن رہی ہوں...';};
  wake_rec.onresult=function(e){
    var t=e.results[0][0].transcript.toLowerCase();
    if(t.indexOf('seerat')!==-1||t.indexOf('سیرت')!==-1||t.indexOf('siraat')!==-1){
      var av=document.getElementById('avDiv');
      av.style.boxShadow='0 0 30px #ff6b9d';av.style.transform='scale(1.15)';
      setTimeout(function(){av.style.boxShadow='';av.style.transform='';},2000);
      setTimeout(function(){mic();},500);
    }
  };
  wake_rec.onerror=function(){wake_on=false;};
  wake_rec.onend=function(){wake_on=false;if(!mic_on)setTimeout(startWakeWord,2000);};
  try{wake_rec.start();}catch(e){}
}

// ===== PANELS =====
function openPanel(type){
  document.getElementById('overlay').classList.add('show');
  ['waPanel','callPanel','alarmPanel'].forEach(function(p){document.getElementById(p).classList.remove('show');});
  if(type==='wa')document.getElementById('waPanel').classList.add('show');
  else if(type==='call')document.getElementById('callPanel').classList.add('show');
  else if(type==='alarm')document.getElementById('alarmPanel').classList.add('show');
}
function closePanel(){
  document.getElementById('overlay').classList.remove('show');
  ['waPanel','callPanel','alarmPanel'].forEach(function(p){document.getElementById(p).classList.remove('show');});
}
function fillWA(num){document.getElementById('waNum').value=num;}
function fillCall(num){document.getElementById('callNum').value=num;}
function sendWA(){
  var num=document.getElementById('waNum').value.trim().replace(/\s/g,'').replace(/\+/g,'');
  var msg=document.getElementById('waMsg').value.trim();
  if(!num){alert('نمبر ڈالیں!');return;}
  window.open('https://wa.me/'+num+(msg?'?text='+encodeURIComponent(msg):''),'_blank');
  am('s','✅ WhatsApp کھل رہا ہے! 💬');closePanel();
}
function makeCall(){
  var num=document.getElementById('callNum').value.trim();
  if(!num){alert('نمبر ڈالیں!');return;}
  window.location.href='tel:'+num;
  am('s','📞 Call شروع ہو رہی ہے...');closePanel();
}

function makeCall(){
  var num=document.getElementById('callNum').value.trim();
  if(!num){alert('نمبر ڈالیں!');return;}
  window.location.href='tel:'+num;
  am('s','📞 Call شروع ہو رہی ہے...');closePanel();
}

// ===== MEMORY SYSTEM =====
var memories=[], learnedItems=[], firstUseDate=null;

function loadMemoryData(){
  var m=localStorage.getItem('seerat_memories');
  var l=localStorage.getItem('seerat_learned');
  var f=localStorage.getItem('seerat_firstuse');
  if(m)try{memories=JSON.parse(m);}catch(e){}
  if(l)try{learnedItems=JSON.parse(l);}catch(e){}
  if(!f){f=new Date().toISOString();localStorage.setItem('seerat_firstuse',f);}
  firstUseDate=f;
  renderMemory();
}

function saveMemoryData(){
  localStorage.setItem('seerat_memories',JSON.stringify(memories));
  localStorage.setItem('seerat_learned',JSON.stringify(learnedItems));
}

function addMemory(){
  var inp=document.getElementById('memInp');
  var txt=inp.value.trim();if(!txt)return;
  memories.push({id:Date.now(),text:txt,time:new Date().toLocaleDateString('ur-PK'),auto:false});
  saveMemoryData();renderMemory();inp.value='';
  am('s','✅ یاد کر لیا! 🧠 "'+txt+'"');
}

function delMemory(id){
  memories=memories.filter(function(m){return m.id!==id;});
  saveMemoryData();renderMemory();
}

function autoLearn(text){
  learnedItems.unshift({id:Date.now(),text:text,time:new Date().toLocaleTimeString('ur-PK',{hour:'2-digit',minute:'2-digit'})});
  if(learnedItems.length>20)learnedItems=learnedItems.slice(0,20);
  saveMemoryData();
}

function renderMemory(){
  var days=Math.floor((new Date()-new Date(firstUseDate||new Date()))/(1000*60*60*24))+1;
  document.getElementById('memCount').textContent=memories.length;
  document.getElementById('learnCount').textContent=learnedItems.length;
  document.getElementById('daysCount').textContent=days;
  var ml=document.getElementById('memList');
  if(!memories.length){ml.innerHTML='<div style="text-align:center;color:rgba(255,255,255,0.3);font-size:12px;padding:12px;direction:rtl;">ابھی کوئی یاد نہیں — نیچے لکھیں!</div>';} 
  else{ml.innerHTML=memories.map(function(m){return '<div class="mem-item"><div><div class="mem-item-text">'+m.text+'</div><div class="mem-item-time">'+m.time+'</div></div><button class="mem-del" onclick="delMemory('+m.id+')">🗑️</button></div>';}).join('');}
  var ll=document.getElementById('learnList');
  if(!learnedItems.length){ll.innerHTML='<div style="text-align:center;color:rgba(255,255,255,0.3);font-size:12px;padding:12px;direction:rtl;">ابھی کچھ نہیں سیکھا</div>';}
  else{ll.innerHTML=learnedItems.slice(0,5).map(function(l){return '<div class="mem-item"><div class="mem-item-text">'+l.text+'</div><div class="mem-item-time">'+l.time+'</div></div>';}).join('');}
}

async function teachSeerat(){
  var what=prompt('سیرت کو کیا سکھانا ہے؟ (مثلاً: میرا نام خیر محمد ہے، میں Tando Jam میں رہتا ہوں)');
  if(!what)return;
  memories.push({id:Date.now(),text:what,time:new Date().toLocaleDateString('ur-PK'),auto:false});
  saveMemoryData();renderMemory();
  am('s','شکریہ! 🧠 میں نے سیکھ لیا: "'+what+'" — اب میں یہ ہمیشہ یاد رکھوں گی! 🌸');
}

// Context-aware memory in chat
function getMemoryContext(){
  if(!memories.length)return '';
  return '\nYaad rahe info: '+memories.map(function(m){return m.text;}).join(', ')+'.';
}

// ===== DAILY SCHEDULE =====
var schedItems=[];

function loadSchedule(){
  var s=localStorage.getItem('seerat_schedule');
  if(s)try{schedItems=JSON.parse(s);}catch(e){}
  var now=new Date();
  var days=['اتوار','پیر','منگل','بدھ','جمعرات','جمعہ','ہفتہ'];
  var months=['جنوری','فروری','مارچ','اپریل','مئی','جون','جولائی','اگست','ستمبر','اکتوبر','نومبر','دسمبر'];
  var el=document.getElementById('schedDate');
  if(el)el.textContent=days[now.getDay()]+' — '+now.getDate()+' '+months[now.getMonth()]+' '+now.getFullYear();
  renderSchedule();
  checkDailyReminder();
}

function saveSchedule(){localStorage.setItem('seerat_schedule',JSON.stringify(schedItems));}

function addSchedule(){
  var task=document.getElementById('schedTask').value.trim();
  var from=document.getElementById('schedFrom').value;
  var to=document.getElementById('schedTo').value;
  if(!task){alert('کام لکھیں!');return;}
  var item={id:Date.now(),task:task,from:from,to:to,done:false,date:new Date().toDateString()};
  schedItems.push(item);
  schedItems.sort(function(a,b){return a.from.localeCompare(b.from);});
  saveSchedule();renderSchedule();
  document.getElementById('schedTask').value='';
  document.getElementById('schedFrom').value='';
  document.getElementById('schedTo').value='';
  // Set reminder
  if(from){
    var now=new Date();var alarm=new Date();
    var p=from.split(':');alarm.setHours(parseInt(p[0]),parseInt(p[1]),0,0);
    if(alarm>now){setTimeout(function(){am('s','⏰ یاد دہانی: ابھی "'+task+'" کا وقت ہے!');spkB('یاد دہانی: '+task);},alarm-now);}
  }
  autoLearn('Schedule میں شامل: '+task+(from?' at '+from:''));
  am('s','✅ Schedule میں شامل ہو گیا: '+task+(from?' ⏰ '+from:''));
}

function toggleSched(id){
  schedItems=schedItems.map(function(s){if(s.id===id)s.done=!s.done;return s;});
  saveSchedule();renderSchedule();
}

function delSched(id){
  schedItems=schedItems.filter(function(s){return s.id!==id;});
  saveSchedule();renderSchedule();
}

function renderSchedule(){
  var el=document.getElementById('schedList');
  if(!el)return;
  var today=new Date().toDateString();
  var todayItems=schedItems.filter(function(s){return s.date===today;});
  if(!todayItems.length){el.innerHTML='<div style="text-align:center;color:rgba(255,255,255,0.3);font-size:13px;padding:20px;direction:rtl;">آج کا کوئی schedule نہیں — اوپر شامل کریں!</div>';return;}
  el.innerHTML=todayItems.map(function(s){
    return '<div class="sched-item'+(s.done?' done':'')+'">'+
      '<div class="sched-item-time">'+(s.from||'--')+(s.to?'<br>'+s.to:'')+'</div>'+
      '<div class="sched-item-text" onclick="toggleSched('+s.id+')">'+s.task+'</div>'+
      '<button class="sched-item-del" onclick="delSched('+s.id+')">🗑️</button></div>';
  }).join('');
  // Tomorrow section
  renderTomorrowReminder(todayItems);
}

function renderTomorrowReminder(items){
  var el=document.getElementById('tomorrowReminder');
  var tl=document.getElementById('tomorrowList');
  if(!el||!tl)return;
  var pending=items.filter(function(s){return !s.done;});
  if(!pending.length){el.style.display='none';return;}
  el.style.display='block';
  tl.innerHTML=pending.map(function(s){return '<div style="font-size:12px;direction:rtl;padding:4px 0;color:rgba(255,255,255,0.7);">• '+(s.from?s.from+' — ':'')+s.task+'</div>';}).join('');
}

function checkDailyReminder(){
  var lastCheck=localStorage.getItem('seerat_lastcheck');
  var today=new Date().toDateString();
  if(lastCheck===today)return;
  localStorage.setItem('seerat_lastcheck',today);
  // Check yesterday's schedule
  var yesterday=new Date();yesterday.setDate(yesterday.getDate()-1);
  var yStr=yesterday.toDateString();
  var yItems=schedItems.filter(function(s){return s.date===yStr;});
  if(yItems.length>0){
    setTimeout(function(){
      var msg='🌅 صبح بخیر! کل آپ نے یہ کام کیے تھے:\n'+yItems.map(function(s){return (s.done?'✅':'⬜')+' '+(s.from?s.from+' — ':'')+s.task;}).join('\n');
      am('s',msg.replace(/\n/g,'<br>'));
      spkB('صبح بخیر! کل کا review سنیں۔');
    },3000);
  }
}

// ===== WEATHER ALERT =====
async function loadWeatherWithAlert(){
  try{
    var r=await fetch('https://api.open-meteo.com/v1/forecast?latitude=25.42&longitude=68.53&current=temperature_2m,weathercode,windspeed_10m&daily=weathercode,temperature_2m_max,temperature_2m_min,precipitation_sum&timezone=Asia/Karachi&forecast_days=2');
    var d=await r.json();
    var temp=Math.round(d.current.temperature_2m);
    var code=d.current.weathercode;
    var wind=d.current.windspeed_10m;
    var desc=code<=1?'صاف موسم ☀️':code<=3?'ابر آلود 🌤️':code<=51?'ہلکی بارش 🌦️':code<=67?'بارش 🌧️':code<=77?'اولے 🌨️':'آندھی ⛈️';
    document.getElementById('weatherTemp').textContent=temp+'°C';
    document.getElementById('weatherCity').textContent='Tando Jam — '+desc;
    // Alert for bad weather
    var alert='';
    if(code>=61&&code<=67)alert='🌧️ موسمی خبردار! آج Tando Jam میں بارش کا امکان ہے۔ چھتری لے جائیں!';
    else if(code>=77&&code<=82)alert='⛈️ خطرناک موسم! آج آندھی اور طوفان کا خدشہ ہے۔ گھر میں رہیں!';
    else if(temp>=42)alert='🌡️ گرمی کا الرٹ! آج درجہ حرارت '+temp+'°C ہے — باہر کم جائیں!';
    else if(temp<=10)alert='🥶 سردی کا الرٹ! آج صرف '+temp+'°C — گرم کپڑے پہنیں!';
    else if(wind>40)alert='💨 تیز ہوا کا الرٹ! ہوا کی رفتار '+Math.round(wind)+' km/h ہے۔';
    var lastAlert=localStorage.getItem('seerat_weatheralert');
    if(alert&&lastAlert!==alert){
      setTimeout(function(){am('s',alert);spkB(alert);},4000);
      localStorage.setItem('seerat_weatheralert',alert);
    }
  }catch(e){document.getElementById('weatherTemp').textContent='--°C';}
}

// ===== GREETING CARDS =====
var cardType='birthday';
var cardDesigns={
  'birthday':{bg:'linear-gradient(135deg,#ff6b9d,#ffd700,#ff6b9d)',ico:'🎂🎉🎁',title:'Happy Birthday!',color:'#fff'},
  'eid':{bg:'linear-gradient(135deg,#006400,#ffd700,#006400)',ico:'🌙⭐🕌',title:'عید مبارک!',color:'#ffd700'},
  'notice':{bg:'linear-gradient(135deg,#1a3a6e,#2a4a8e)',ico:'📢🏫📋',title:'School Notice',color:'#88ccff'},
  'custom':{bg:'linear-gradient(135deg,#6c3483,#1a0a2e,#2d1554)',ico:'✨🌸💫',title:'Special Message',color:'#ff6b9d'}
};

function selectCardType(type){
  cardType=type;
  document.querySelectorAll('.card-type').forEach(function(el){el.classList.remove('selected');});
  document.getElementById('ctype-'+type).classList.add('selected');
  updateCardPreview();
}

function updateCardPreview(){
  var name=document.getElementById('cardName').value||'آپ کا نام';
  var design=cardDesigns[cardType];
  var prev=document.getElementById('cardPreview');
  prev.style.background=design.bg;
  var msgs={
    'birthday':'پیارے '+name+'! آپ کو دل کی گہرائیوں سے سالگرہ مبارک! 🌸 اللہ آپ کی ہر خواہش پوری فرمائے!',
    'eid':'محترم '+name+'! عید مبارک! 🌙 اللہ تعالیٰ آپ کی قربانی قبول فرمائے اور آپ پر رحمتیں نازل فرمائے!',
    'notice':name+' — '+new Date().toLocaleDateString('ur-PK')+' کا اہم نوٹس۔ براہ کرم توجہ سے پڑھیں۔',
    'custom':'محترم '+name+'! آپ کے لیے ایک خاص پیغام۔ 💫'
  };
  prev.innerHTML='<div class="card-preview-ico">'+design.ico.split('')[0]+'</div>'+
    '<div class="card-preview-title" style="color:'+design.color+'">'+design.title+'</div>'+
    '<div class="card-preview-msg">'+msgs[cardType]+'</div>'+
    '<div class="card-preview-from" style="color:'+design.color+'">— Al-Fareed Public School, Tando Jam</div>';
}

async function generateCard(){
  var name=document.getElementById('cardName').value.trim();
  if(!name){alert('نام لکھیں!');return;}
  if(!AK){alert('API key ضروری ہے!');return;}
  var typeNames={'birthday':'سالگرہ','eid':'عید','notice':'اسکول نوٹس','custom':'خاص پیغام'};
  var prompt='ایک خوبصورت '+typeNames[cardType]+' card کا پیغام لکھو "'+name+'" کے لیے۔ اردو میں، دل سے، 3-4 جملے، emoji کے ساتھ۔ صرف پیغام لکھو، کچھ اور نہیں۔';
  var btn=document.querySelector('.card-gen-btn');btn.textContent='⏳ بن رہا ہے...';
  try{
    var r=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json','x-api-key':AK,'anthropic-version':'2023-06-01'},body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:300,messages:[{role:'user',content:prompt}]})});
    var d=await r.json();
    if(d.content&&d.content[0]){
      var msg=d.content[0].text;
      document.getElementById('cardMsg').value=msg;
      var design=cardDesigns[cardType];
      var prev=document.getElementById('cardPreview');
      prev.style.background=design.bg;
      prev.innerHTML='<div class="card-preview-ico">'+design.ico.split('')[0]+'</div>'+
        '<div class="card-preview-title" style="color:'+design.color+'">'+design.title+'</div>'+
        '<div class="card-preview-msg">'+msg+'</div>'+
        '<div class="card-preview-from" style="color:'+design.color+'">— Al-Fareed Public School, Tando Jam</div>';
    }
  }catch(e){alert('خرابی — دوبارہ کوشش کریں');}
  btn.textContent='✨ AI سے Card بنوائیں';
}

function sendCardWA(){
  var name=document.getElementById('cardName').value.trim();
  var msg=document.getElementById('cardMsg').value.trim();
  var num=document.getElementById('cardWaNum').value.trim().replace(/\s/g,'').replace(/\+/g,'');
  if(!num){alert('WhatsApp نمبر ڈالیں!');return;}
  var design=cardDesigns[cardType];
  var typeNames={'birthday':'🎂 سالگرہ مبارک','eid':'🌙 عید مبارک','notice':'📢 School Notice','custom':'✨ خاص پیغام'};
  var fullMsg=typeNames[cardType]+'\n\n'+(msg||'آپ کے لیے دعائیں! 🌸')+'\n\n— Al-Fareed Public School, Tando Jam\n'+design.ico;
  var url='https://wa.me/'+num+'?text='+encodeURIComponent(fullMsg);
  window.open(url,'_blank');
  am('s','✅ WhatsApp کھل رہا ہے! '+name+' کو card بھیجیں! 💬');
  autoLearn('Card بھیجا: '+typeNames[cardType]+' to '+name);
}

// ===== TEACHER AI =====
var tMode='word';
function setTMode(m){
  tMode=m;
  document.querySelectorAll('.tmode').forEach(function(el){el.classList.remove('selected');});
  document.getElementById('tmode-'+m).classList.add('selected');
  var topics={
    'word':['📚 Photosynthesis','🏛️ Democracy','⚛️ Atom','✍️ Metaphor','🌍 Geography','📖 Allegory'],
    'math':['📐 2x+5=15','🔢 3²+4²=?','📊 دائرے کا رقبہ r=7','➗ 144÷12','📏 Pythagoras','🔣 Quadratic'],
    'science':['🌿 Photosynthesis','⚛️ Atom','🧬 DNA','🌊 Water Cycle','🔋 Battery','❤️ Heart'],
    'explain':['🌍 Climate Change','💻 Internet','🌙 چاند','✈️ ہوائی جہاز','🧠 Memory','📱 Mobile']
  };
  var t=topics[m]||[];
  document.getElementById('quickTopics').innerHTML=t.map(function(tp){
    return '<button class="qtopic" onclick="teacherAsk(\''+tp.replace(/'/g,"\\'")+'\')">' + tp + '</button>';
  }).join('');
}

function teacherAsk(q){
  document.getElementById('teacherTb').value=q;
  teacherSend();
}

function tAddMsg(type,html){
  var c=document.getElementById('teacherChat');
  var d=document.createElement('div');
  d.className='slide-card slide-user';
  d.innerHTML='<div style="font-size:13px;direction:rtl;text-align:right;padding-right:24px;">'+html+'</div>';
  c.appendChild(d);c.scrollTop=c.scrollHeight;
}

function tShowLoad(){
  var c=document.getElementById('teacherChat');
  var d=document.createElement('div');d.id='tload';
  d.className='slide-card slide-loading';
  d.innerHTML='<div class="loading-teacher">👩‍🏫</div><div class="loading-text">استاد سوچ رہی ہیں...</div><div class="tload"><span></span><span></span><span></span></div>';
  c.appendChild(d);c.scrollTop=c.scrollHeight;
}
function tHideLoad(){var t=document.getElementById('tload');if(t)t.remove();}

async function teacherSend(){
  var b=document.getElementById('teacherTb');
  var q=b.value.trim();if(!q)return;b.value='';
  tAddMsg('u',q);
  if(!AK){renderSlide('explain',{oneliner:'⚠️ API key نہیں!',detail:'اوپر Keys تبدیل کریں دبائیں'});return;}
  tShowLoad();
  var wp={
    'word':'تم ماہر استاد ہو۔ لفظ: "'+q+'"۔ صرف JSON دو بغیر کسی اور text کے:\n{"word":"لفظ","lang":"زبان","lang_detail":"کس زبان سے کیوں","history":"تاریخ 2-3 جملے اردو","meaning":"مکمل مطلب اردو","examples":["جملہ1","جملہ2","جملہ3"],"related":["s1","s2","s3"]}',
    'math':'تم Math استاد ہو۔ سوال: "'+q+'"۔ صرف JSON دو:\n{"question":"سوال","method":"طریقہ","steps":["قدم1","قدم2","قدم3","قدم4"],"answer":"جواب","rule":"اہم rule اردو میں"}',
    'science':'تم Science استاد ہو۔ Topic: "'+q+'"۔ صرف JSON دو:\n{"topic":"topic","definition":"تعریف اردو","process":["عمل1","عمل2","عمل3"],"example":"مثال","fact":"دلچسپ fact","diagram":"yes"}',
    'explain':'تم ذہین استاد ہو۔ Topic: "'+q+'"۔ صرف JSON دو:\n{"topic":"topic","oneliner":"ایک جملہ","detail":"3-4 جملے اردو","example":"گھریلو مثال","fact":"حیران کن بات","related":["t1","t2","t3"]}'
  };
  try{
    var r=await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':AK,'anthropic-version':'2023-06-01'},
      body:JSON.stringify({model:'claude-sonnet-4-20250514',max_tokens:1000,messages:[{role:'user',content:wp[tMode]||wp['explain']}]})
    });
    var d=await r.json();tHideLoad();
    if(d.content&&d.content[0]&&d.content[0].text){
      var txt=d.content[0].text.replace(/```json|```/g,'').trim();
      try{var data=JSON.parse(txt);renderSlide(tMode,data);}
      catch(e){
        var fc=document.getElementById('teacherChat');
        var fd=document.createElement('div');fd.className='slide-card slide-explain';
        fd.innerHTML='<div class="se-detail">'+txt.replace(/\n/g,'<br>')+'</div>';
        fc.appendChild(fd);fc.scrollTop=fc.scrollHeight;
      }
    }
  }catch(e){tHideLoad();renderSlide('explain',{oneliner:'⚠️ خرابی',detail:'Internet یا API key چیک کریں!'});}
}

function renderSlide(mode,data){
  var c=document.getElementById('teacherChat');
  var d=document.createElement('div');
  if(mode==='word'){
    d.className='slide-card slide-word';
    var ex=(data.examples||[]).map(function(e,i){return '<div style="margin:3px 0;padding:5px 8px;background:rgba(255,255,255,0.05);border-radius:6px;direction:rtl;">'+(i+1)+'. '+e+'</div>';}).join('');
    var rel=(data.related||[]).map(function(r){return '<span class="tag">'+r+'</span>';}).join('');
    d.innerHTML='<span class="sw-badge">📚 لفظ کا سبق</span>'+
      '<div class="sw-title">'+(data.word||'')+'</div>'+
      '<div class="sw-lang">🌍 '+(data.lang||'')+' — '+(data.lang_detail||'')+'</div>'+
      '<div class="sw-section sw-history"><span class="sw-sec-title">📖 تاریخ</span><div class="sw-sec-body">'+(data.history||'')+'</div></div>'+
      '<div class="sw-section sw-meaning"><span class="sw-sec-title">💡 مطلب</span><div class="sw-sec-body">'+(data.meaning||'')+'</div></div>'+
      '<div class="sw-section sw-usage"><span class="sw-sec-title">✏️ جملوں میں</span><div class="sw-sec-body">'+ex+'</div></div>'+
      '<div class="sw-section sw-related"><span class="sw-sec-title">🔗 ملتے جلتے</span><div class="sw-sec-body">'+rel+'</div></div>';
  } else if(mode==='math'){
    d.className='slide-card slide-math';
    var st=(data.steps||[]).map(function(s,i){return '<div class="sm-step"><div class="sm-step-num">'+(i+1)+'</div><div class="sm-step-body">'+s+'</div></div>';}).join('');
    d.innerHTML='<span class="sw-badge" style="background:#4488ff;">🔢 ریاضی حل</span>'+
      '<div class="sm-question">'+(data.question||'')+'</div>'+
      '<div style="font-size:11px;color:#88ccff;direction:rtl;margin-bottom:8px;">📐 طریقہ: '+(data.method||'')+'</div>'+
      '<div class="sm-steps">'+st+'</div>'+
      '<div class="sm-answer"><div class="sm-answer-label">✅ حتمی جواب</div><div class="sm-answer-val">'+(data.answer||'')+'</div></div>'+
      '<div style="font-size:11px;color:rgba(255,255,255,0.5);direction:rtl;margin-top:8px;padding:6px 10px;background:rgba(255,255,255,0.04);border-radius:8px;">💡 یاد رکھیں: '+(data.rule||'')+'</div>';
  } else if(mode==='science'){
    d.className='slide-card slide-science';
    var ic=['🔹','🔸','🔷','🔶','⭐'];
    var pr=(data.process||[]).map(function(p,i){return '<div class="ss-point"><span class="ss-point-ico">'+(ic[i]||'▪️')+'</span><div class="ss-point-text">'+p+'</div></div>';}).join('');
    d.innerHTML='<span class="sw-badge" style="background:#44cc88;color:#000;">🔬 سائنس سبق</span>'+
      '<div style="font-size:16px;font-weight:bold;color:#44ff88;direction:rtl;margin-bottom:10px;">'+(data.topic||'')+'</div>'+
      '<div class="ss-def">'+(data.definition||'')+'</div>'+
      '<div style="font-size:11px;color:#44cc88;direction:rtl;margin-bottom:6px;">⚙️ کام کا طریقہ:</div>'+
      '<div class="ss-points">'+pr+'</div>'+
      '<div style="background:rgba(255,200,50,0.1);border:1px solid rgba(255,200,50,0.3);border-radius:10px;padding:8px 12px;direction:rtl;margin-top:8px;font-size:13px;">🏠 مثال: '+(data.example||'')+'</div>'+
      '<div style="background:rgba(200,100,255,0.1);border-radius:8px;padding:7px 10px;direction:rtl;margin-top:6px;font-size:12px;color:#cc88ff;">🤩 '+(data.fact||'')+'</div>';
    c.appendChild(d);c.scrollTop=c.scrollHeight;
    if(data.diagram==='yes'){setTimeout(function(){drawScienceDiagram(data.topic||'');},200);}
    return;
  } else {
    d.className='slide-card slide-explain';
    var rt=(data.related||[]).map(function(r){return '<span class="tag">'+r+'</span>';}).join('');
    d.innerHTML='<span class="sw-badge" style="background:#ffcc22;color:#000;">💡 وضاحت</span>'+
      '<div class="se-oneliner">'+(data.oneliner||data.topic||'')+'</div>'+
      '<div class="se-detail">'+(data.detail||'')+'</div>'+
      (data.example?'<div class="se-example"><div class="se-example-label">🏠 مثال:</div><div class="se-example-text">'+(data.example)+'</div></div>':'')+
      (data.fact?'<div class="se-fact"><span class="se-fact-label">🤩 دلچسپ: </span>'+(data.fact)+'</div>':'')+
      (rt?'<div style="margin-top:8px;">'+rt+'</div>':'');
  }
  c.appendChild(d);c.scrollTop=c.scrollHeight;
}

function drawScienceDiagram(topic){
  var c=document.getElementById('teacherChat');
  var wrap=document.createElement('div');wrap.style.cssText='background:rgba(255,255,255,0.04);border:1px solid rgba(255,107,157,0.2);border-radius:12px;padding:12px;margin:6px 0;';
  wrap.innerHTML='<div style="font-size:12px;color:#ff6b9d;margin-bottom:8px;direction:rtl;text-align:right;">📊 '+topic+' — خاکہ</div>';
  var canvas=document.createElement('canvas');canvas.width=320;canvas.height=220;canvas.style.cssText='width:100%;max-width:320px;border-radius:8px;display:block;margin:0 auto;';
  wrap.appendChild(canvas);c.appendChild(wrap);c.scrollTop=c.scrollHeight;
  var ctx=canvas.getContext('2d');
  var tl=topic.toLowerCase();
  if(tl.indexOf('atom')!==-1||tl.indexOf('ایٹم')!==-1){drawAtom(ctx,320,220);}
  else if(tl.indexOf('photo')!==-1||tl.indexOf('ضیاء')!==-1){drawPhotosynthesis(ctx,320,220);}
  else if(tl.indexOf('water')!==-1||tl.indexOf('cycle')!==-1||tl.indexOf('آبی')!==-1){drawWaterCycle(ctx,320,220);}
  else if(tl.indexOf('heart')!==-1||tl.indexOf('دل')!==-1){drawHeart(ctx,320,220);}
  else if(tl.indexOf('cell')!==-1||tl.indexOf('خلیہ')!==-1){drawCell(ctx,320,220);}
  else if(tl.indexOf('osmosis')!==-1){drawOsmosis(ctx,320,220);}
  else if(tl.indexOf('dna')!==-1){drawDNA(ctx,320,220);}
  else{drawGeneric(ctx,320,220,topic);}
}

function drawAtom(ctx,w,h){
  var cx=w/2,cy=h/2;
  ctx.fillStyle='#050510';ctx.fillRect(0,0,w,h);
  ctx.beginPath();ctx.arc(cx,cy,22,0,Math.PI*2);ctx.fillStyle='#cc2244';ctx.fill();
  ctx.fillStyle='white';ctx.font='bold 10px Arial';ctx.textAlign='center';ctx.fillText('Nucleus',cx,cy+4);
  var orbs=[{rx:70,ry:28,a:0},{rx:55,ry:45,a:60},{rx:75,ry:22,a:120}];
  orbs.forEach(function(o,i){
    ctx.save();ctx.translate(cx,cy);ctx.rotate(o.a*Math.PI/180);
    ctx.beginPath();ctx.ellipse(0,0,o.rx,o.ry,0,0,Math.PI*2);
    ctx.strokeStyle='rgba(100,180,255,0.5)';ctx.lineWidth=1.5;ctx.stroke();
    var ang=(i*120)*Math.PI/180;
    ctx.beginPath();ctx.arc(o.rx*Math.cos(ang),o.ry*Math.sin(ang),7,0,Math.PI*2);
    ctx.fillStyle='#00ff88';ctx.fill();ctx.restore();
  });
  ctx.fillStyle='rgba(255,255,255,0.6)';ctx.font='10px Arial';ctx.textAlign='left';
  ctx.fillText('🟢 الیکٹران',8,18);
  ctx.fillStyle='#cc2244';ctx.fillText('🔴 مرکزہ',8,32);
  ctx.fillStyle='rgba(100,180,255,0.8)';ctx.fillText('○ مدار',8,46);
  ctx.fillStyle='#ff6b9d';ctx.font='bold 12px Arial';ctx.textAlign='center';ctx.fillText('ایٹم — Atom',cx,h-6);
}

function drawPhotosynthesis(ctx,w,h){
  ctx.fillStyle='#081408';ctx.fillRect(0,0,w,h);
  ctx.beginPath();ctx.ellipse(w/2,h/2,90,55,Math.PI/10,0,Math.PI*2);ctx.fillStyle='#1a4a0a';ctx.fill();ctx.strokeStyle='#2d8a14';ctx.lineWidth=2;ctx.stroke();
  ctx.beginPath();ctx.moveTo(w/2-75,h/2+20);ctx.lineTo(w/2+75,h/2-20);ctx.strokeStyle='rgba(80,180,40,0.5)';ctx.lineWidth=2;ctx.stroke();
  ctx.beginPath();ctx.arc(45,35,22,0,Math.PI*2);ctx.fillStyle='#ffd700';ctx.fill();
  // Light rays
  ctx.strokeStyle='rgba(255,215,0,0.5)';ctx.lineWidth=1.5;
  [[60,45,w/2-40,h/2-20],[55,52,w/2-20,h/2-10],[65,58,w/2-60,h/2]].forEach(function(l){ctx.beginPath();ctx.moveTo(l[0],l[1]);ctx.lineTo(l[2],l[3]);ctx.stroke();});
  // CO2 arrows
  ctx.strokeStyle='rgba(200,200,100,0.6)';ctx.lineWidth=1.5;
  ctx.beginPath();ctx.moveTo(w-20,h/2);ctx.lineTo(w/2+50,h/2);ctx.stroke();
  // O2 arrows
  ctx.strokeStyle='rgba(100,200,255,0.6)';
  ctx.beginPath();ctx.moveTo(w/2,h/2-55);ctx.lineTo(w/2,20);ctx.stroke();
  ctx.fillStyle='#ffd700';ctx.font='10px Arial';ctx.textAlign='left';ctx.fillText('☀️ روشنی',5,20);
  ctx.fillStyle='rgba(200,200,100,0.9)';ctx.fillText('CO₂ + H₂O',w-80,h/2-5);
  ctx.fillStyle='rgba(100,200,255,0.9)';ctx.fillText('O₂',w/2+5,18);
  ctx.fillStyle='#00ff88';ctx.fillText('Glucose',w/2-30,h-8);
  ctx.fillStyle='#2d8a14';ctx.font='bold 11px Arial';ctx.textAlign='center';ctx.fillText('ضیاء ترکیب — Photosynthesis',w/2,h-20);
}

function drawWaterCycle(ctx,w,h){
  ctx.fillStyle='#080818';ctx.fillRect(0,0,w,h);
  ctx.fillStyle='#1a3020';ctx.fillRect(0,h-45,w,45);
  ctx.fillStyle='#0a2040';ctx.fillRect(0,h-45,120,25);
  // Sun
  ctx.beginPath();ctx.arc(w-45,35,25,0,Math.PI*2);ctx.fillStyle='#ffa500';ctx.fill();
  ctx.fillStyle='white';ctx.font='14px Arial';ctx.textAlign='center';ctx.fillText('☀',w-45,40);
  // Cloud
  ctx.fillStyle='#8899aa';
  [[w/2,60,28],[w/2+25,55,22],[w/2-22,60,20],[w/2+8,68,18]].forEach(function(c){ctx.beginPath();ctx.arc(c[0],c[1],c[2],0,Math.PI*2);ctx.fill();});
  // Rain
  ctx.strokeStyle='#6699ff';ctx.lineWidth=2;
  for(var i=0;i<5;i++){ctx.beginPath();ctx.moveTo(w/2-20+i*10,85);ctx.lineTo(w/2-24+i*10,100);ctx.stroke();}
  // Evaporation arrows
  ctx.strokeStyle='rgba(255,150,50,0.6)';ctx.lineWidth=2;
  ctx.beginPath();ctx.moveTo(60,h-55);ctx.quadraticCurveTo(20,h/2-20,w/2-30,70);ctx.stroke();
  // Labels
  ctx.fillStyle='rgba(255,150,50,0.9)';ctx.font='10px Arial';ctx.textAlign='left';ctx.fillText('بخارات',5,h/2-10);
  ctx.fillStyle='#6699ff';ctx.fillText('بارش (Rain)',w/2+10,95);
  ctx.fillStyle='#2a6040';ctx.fillText('زمین',5,h-28);
  ctx.fillStyle='#0a4080';ctx.fillText('پانی',5,h-48);
  ctx.fillStyle='white';ctx.font='bold 11px Arial';ctx.textAlign='center';ctx.fillText('آبی چکر — Water Cycle',w/2,h-5);
}

function drawHeart(ctx,w,h){
  ctx.fillStyle='#100008';ctx.fillRect(0,0,w,h);
  var cx=w/2,cy=h/2+5;
  ctx.beginPath();ctx.moveTo(cx,cy+50);
  ctx.bezierCurveTo(cx-90,cy+10,cx-90,cy-45,cx,cy-15);
  ctx.bezierCurveTo(cx+90,cy-45,cx+90,cy+10,cx,cy+50);
  ctx.fillStyle='#aa1133';ctx.fill();ctx.strokeStyle='#ff3355';ctx.lineWidth=2;ctx.stroke();
  ctx.beginPath();ctx.moveTo(cx,cy-15);ctx.lineTo(cx,cy+50);ctx.strokeStyle='rgba(255,255,255,0.25)';ctx.lineWidth=2;ctx.stroke();
  ctx.beginPath();ctx.moveTo(cx-45,cy+10);ctx.lineTo(cx+45,cy+10);ctx.stroke();
  ctx.fillStyle='rgba(255,255,255,0.85)';ctx.font='9px Arial';ctx.textAlign='center';
  ctx.fillText('Right Atrium',cx-28,cy-5);ctx.fillText('Left Atrium',cx+28,cy-5);
  ctx.fillText('Right Ventricle',cx-28,cy+30);ctx.fillText('Left Ventricle',cx+28,cy+30);
  ctx.fillStyle='#ff6b9d';ctx.font='bold 12px Arial';ctx.fillText('دل — Heart',cx,h-5);
}

function drawCell(ctx,w,h){
  ctx.fillStyle='#05050f';ctx.fillRect(0,0,w,h);
  var cx=w/2,cy=h/2;
  ctx.beginPath();ctx.ellipse(cx,cy,120,80,0,0,Math.PI*2);ctx.strokeStyle='#4488ff';ctx.lineWidth=3;ctx.stroke();ctx.fillStyle='rgba(68,136,255,0.04)';ctx.fill();
  ctx.beginPath();ctx.ellipse(cx,cy,32,26,0,0,Math.PI*2);ctx.fillStyle='rgba(255,107,157,0.25)';ctx.fill();ctx.strokeStyle='#ff6b9d';ctx.lineWidth=2;ctx.stroke();
  ctx.fillStyle='#ff6b9d';ctx.font='bold 9px Arial';ctx.textAlign='center';ctx.fillText('Nucleus',cx,cy+4);
  [[cx-65,cy-18,'Mitochondria','#00ff88'],[cx+65,cy+20,'Ribosome','#ffd700'],[cx-35,cy+45,'Vacuole','#87ceeb'],[cx+40,cy-42,'Chloroplast','#44cc44']].forEach(function(o){
    ctx.beginPath();ctx.ellipse(o[0],o[1],20,13,0,0,Math.PI*2);ctx.fillStyle=o[3]+'33';ctx.fill();ctx.strokeStyle=o[3];ctx.lineWidth=1.5;ctx.stroke();
    ctx.fillStyle=o[3];ctx.font='8px Arial';ctx.fillText(o[2],o[0],o[1]+3);
  });
  ctx.fillStyle='#4488ff';ctx.font='bold 11px Arial';ctx.textAlign='center';ctx.fillText('خلیہ — Cell',cx,h-5);
}

function drawOsmosis(ctx,w,h){
  ctx.fillStyle='#050510';ctx.fillRect(0,0,w,h);
  // Membrane
  ctx.fillStyle='rgba(255,107,157,0.2)';ctx.fillRect(w/2-8,20,16,h-40);ctx.strokeStyle='#ff6b9d';ctx.lineWidth=2;
  ctx.strokeRect(w/2-8,20,16,h-40);
  // Water molecules left
  ctx.fillStyle='rgba(100,180,255,0.6)';
  [[50,50],[70,80],[40,110],[80,130],[55,160],[75,190]].forEach(function(p){ctx.beginPath();ctx.arc(p[0],p[1],8,0,Math.PI*2);ctx.fill();});
  // Solute right side
  ctx.fillStyle='rgba(255,200,100,0.8)';
  [[220,60],[240,100],[210,140],[230,170],[250,120],[220,200]].forEach(function(p){ctx.beginPath();ctx.arc(p[0],p[1],6,0,Math.PI*2);ctx.fill();});
  ctx.fillStyle='rgba(100,180,255,0.4)';
  [[200,70],[210,110],[200,150],[215,185]].forEach(function(p){ctx.beginPath();ctx.arc(p[0],p[1],8,0,Math.PI*2);ctx.fill();});
  // Arrows
  ctx.strokeStyle='rgba(100,180,255,0.8)';ctx.lineWidth=2;
  ctx.beginPath();ctx.moveTo(w/2-25,h/2);ctx.lineTo(w/2+8,h/2);ctx.stroke();
  ctx.beginPath();ctx.moveTo(w/2+5,h/2-5);ctx.lineTo(w/2+15,h/2);ctx.lineTo(w/2+5,h/2+5);ctx.stroke();
  ctx.fillStyle='rgba(100,180,255,0.9)';ctx.font='10px Arial';ctx.textAlign='right';ctx.fillText('خالص پانی',w/2-12,h/2-5);
  ctx.fillStyle='rgba(255,200,100,0.9)';ctx.textAlign='left';ctx.fillText('محلول',w/2+20,h/2-5);
  ctx.fillStyle='#ff6b9d';ctx.font='9px Arial';ctx.textAlign='center';ctx.fillText('نیم قابل نفوذ جھلی',w/2,h-8);
  ctx.fillStyle='white';ctx.font='bold 11px Arial';ctx.fillText('Osmosis — ا سموسس',w/2,12);
}

function drawDNA(ctx,w,h){
  ctx.fillStyle='#030310';ctx.fillRect(0,0,w,h);
  var cx=w/2;
  for(var i=0;i<18;i++){
    var y=15+i*12;var x=Math.sin(i*0.7)*50;
    ctx.beginPath();ctx.arc(cx-40+x,y,5,0,Math.PI*2);ctx.fillStyle=i%2===0?'#ff6b9d':'#00ff88';ctx.fill();
    ctx.beginPath();ctx.arc(cx+40-x,y,5,0,Math.PI*2);ctx.fillStyle=i%2===0?'#ffd700':'#87ceeb';ctx.fill();
    ctx.beginPath();ctx.moveTo(cx-35+x,y);ctx.lineTo(cx+35-x,y);ctx.strokeStyle='rgba(255,255,255,0.2)';ctx.lineWidth=1;ctx.stroke();
  }
  ctx.strokeStyle='rgba(255,107,157,0.6)';ctx.lineWidth=2;
  ctx.beginPath();for(var j=0;j<50;j++){ctx.lineTo(cx-40+Math.sin(j*0.7)*50,15+j*5);}ctx.stroke();
  ctx.strokeStyle='rgba(100,255,200,0.6)';
  ctx.beginPath();for(var k=0;k<50;k++){ctx.lineTo(cx+40-Math.sin(k*0.7)*50,15+k*5);}ctx.stroke();
  ctx.fillStyle='#ff6b9d';ctx.font='bold 12px Arial';ctx.textAlign='center';ctx.fillText('DNA — ڈی این اے',cx,h-5);
}

function drawGeneric(ctx,w,h,topic){
  ctx.fillStyle='#1a0a2e';ctx.fillRect(0,0,w,h);
  ctx.strokeStyle='rgba(255,107,157,0.2)';ctx.lineWidth=1;
  for(var i=1;i<=5;i++){ctx.beginPath();ctx.arc(w/2,h/2,i*22,0,Math.PI*2);ctx.stroke();}
  ctx.fillStyle='rgba(255,107,157,0.15)';ctx.beginPath();ctx.arc(w/2,h/2,22,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#ff6b9d';ctx.font='bold 13px Arial';ctx.textAlign='center';ctx.fillText(topic,w/2,h/2+5);
  ctx.fillStyle='rgba(255,255,255,0.4)';ctx.font='10px Arial';ctx.fillText('خاکہ — Diagram',w/2,h-8);
}
</script>
</body>
</html>
