 // ==UserScript==
// @name         Перезагрузка игры
// @namespace    http://tampermonkey.net/
// @version      2025-04-10
// @description  Перезагрузка
// @author       You
// @match        https://mine-craft.io/
// @icon         https://www.google.com/s2/favicons?sz=64&domain=mine-craft.io
// @grant        none
//Перезагрузчик игры на tamper monkey
//если вы не играете в эту игру то можете изменить  @match на свою игру
// ==/UserScript==

(function() {
    'use strict';


(function(){
	'use strict';
	setInterval(function(){document.location.reload()}, 2000)
	// Перезагружает игру ( 2000 = 2 секунде 20000 = 20 секундам и т.д )
})();
})();
