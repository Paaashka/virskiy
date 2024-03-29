+++
title = "Нежадные (ungreedy) регулярные выражения в Javascript"
date = 2010-12-08T00:00:00+03:00
tags = ["javascript", "regexp"]
summary = "Как писать нежадные регулярные выражения в JS"
+++

{{< oldpost >}}

Привет.

Как вы, наверное, знаете, джаваскрипт не поддерживает никакие другие модификаторы шаблонов регулярных выражений, 
кроме «g» (глобальная подстановка), «i» (игнорировать регистр символов) и «m» (многострочная подстановка).
В частности, нет такого полезного модификатора, как «Ungreedy». Но, как оказалось, его можно включить, но немного по-другому.

Например у нас есть задача: заменить все `{$var}` в строке `Some variable here: {$var} and there: {$var}` на `<a>var</a>`. 
Если мы попробуем использовать регулярное выражение `/{\$(.*)}/g`, то получим следующее: 
`Some variable here: <a>var} and there: {$var</a>`, что явно нам не подходит. 
Это произошло потому, что по-умолчанию в JS регулярные выражения «жадные» — т.е. пытаются взять максимально подходящее 
под шаблон количество символов. В нашем случае под шаблон подошла вся строка от первого `{$` до последнего `}`. 
Нам же нужно другое поведение.

Для этого используем хитрое сочетание специальных символов(подсмотренное в MDN), и наш шаблон обретает следующий 
вид: `/{\$(.+?)}/g`. Теперь при замене мы получаем именно то, что нам требуется 
`Some variable here: <a>var</a> and there: <a>var</a>`.

Удачи!
