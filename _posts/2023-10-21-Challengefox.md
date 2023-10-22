---
title: Challengefox - Flag4All 2023
date: 2023-10-21 +0200
tags: [Web security, Php, Code audit]
categories: [Write-ups]
---

# Introduction:

![i3](../../assets/flag4all/challengefox.png)

The "Challenge Fox" is a PHP-based web challenge that tests participants' understanding of PHP quirks, string manipulation, and hash vulnerabilities. The challenge consists of four main steps, each requiring a unique approach to solve.

## Step 1: Code Deobfuscation

Upon first inspection, the provided PHP code is obfuscated using hexadecimal representations of characters. This makes the code unreadable and challenging to understand.

```php
 <?php
goto rjJoj;
l5p8t:
$variable = str_replace("\143\x68\141\154\154\145\x6e\147\x65\146\x6f\x78", '', $variable);
goto MGxdQ;
lIReG:
function echec()
{
goto jCY0w;
Dm3Uc:
source();
goto pj4hI;
jCY0w:
echo "\x45\143\x68\x65\143\x2e\x20\74\x62\x72\40\57\76";
goto Dm3Uc;
pj4hI:
exit;
goto gPDe0;
gPDe0:
}
goto lbiZM;
bOncl:
if ($variable === "\143\x68\141\x6c\154\145\156\147\145\146\157\x78") {
echo "\x2d\x20\123\x69\40\143\145\x20\x74\x65\170\164\x65\x20\x61\x70\x70\x61\x72\x61\151\164\54\x20\x74\165\40\166\x61\154\x69\x64\x65\40\x6c\x61\x20\160\x72\x65\x6d\151\x65\162\x65\40\x65\x74\141\x70\x65\41\40\74\x62\x72\76";
if (isset($_GET["\143\150\x61\x6c\154\x65\x6e\147\x65\137\x66\157\x78"])) {
echo "\x2d\x20\104\145\165\x78\151\x65\155\x65\40\145\x74\141\160\145\x20\x76\141\154\x69\x64\145\41\x20\x3c\x62\162\x3e";
if (hash("\155\x64\x32", $_GET["\x76\141\x72\151\141\x62\x6c\x65\x32"]) == "\60") {
echo "\55\x20\124\x72\x6f\151\163\x69\x65\155\145\x20\145\164\141\160\x65\40\166\x61\x6c\151\x64\145\x21\x20\74\142\x72\x3e";
if (hash("\x73\x68\141\x31", $_GET["\166\x61\x72\x69\141\x62\154\145\x33"]) == $_GET["\x76\x61\x72\151\141\142\154\145\63"]) {
echo "\55\40\x4f\153\x61\171\x2c\40\x76\x6f\151\x63\151\40\154\145\x20\146\154\x61\147\40\x3a\x20" . $secretflag . "\74\142\x72\x3e";
}
}
}
}
goto nKESF;
HVY3V:
echo "\74\x70\x3e\x41\x6e\x61\x6c\171\x73\x65\x72\x20\154\x65\x20\143\157\x64\145\40\143\151\40\x64\x65\x73\x73\x6f\x75\163\x20\145\x74\x20\x74\x72\157\165\166\145\x72\x20\x6c\145\40\x6d\x6f\x79\x65\x6e\40\x64\40\x61\x66\x66\x69\x63\x68\x65\x72\x20\x6c\x65\x20\x66\154\141\x67\x2e\74\160\76";
goto g9hQi;
lbiZM:
$variable = $_GET["\166\141\x72\x69\141\142\154\145"];
goto l5p8t;
Oz2JG:
echo "\x3c\164\151\x74\154\145\76\x43\x68\x61\154\154\145\156\147\x65\40\x46\157\x78\x3c\x2f\164\151\x74\154\x65\76";
goto E0h5E;
MGxdQ:
$query = urldecode($_SERVER["\x51\x55\x45\122\x59\x5f\123\x54\122\x49\x4e\x47"]);
goto Z_G58;
MYfqC:
function source()
{
goto nUBkJ;
pqZ02:
highlight_string(file_get_contents(__FILE__));
goto P9KZ3;
nUBkJ:
echo "\x3c\x62\162\76\x3c\143\x6f\144\145\76";
goto pqZ02;
P9KZ3:
echo "\74\x2f\x63\157\144\145\76";
goto NTzIV;
NTzIV:
}
goto lIReG;
E0h5E:
echo "\74\x62\x3e\x43\150\x61\154\154\x65\x6e\x67\x65\40\106\157\x78\74\x2f\x62\76";
goto HVY3V;
Z_G58:
if (preg_match("\x2f\x20\174\137\x2f", $query)) {
echec();
}
goto bOncl;
g9hQi:
echo "\74\142\x72\76\x3c\110\x52\76\x3c\142\162\76";
goto MYfqC;
rjJoj:
include "\146\x6c\x61\147\x2e\160\150\x70";
goto Oz2JG;
nKESF:
source(); 
```

**Solution:** One could use various online tools or scripts to convert these hexadecimal values back to their ASCII counterparts.

This gives us the following code :

```php
<?php

goto start;
step1:
$variable = str_replace("challengefox", '', $variable);
goto step2;
echec:
function echec()
{
    echo "Echec. <br />";
    source();
    exit;
}
step2:
$variable = $_GET["variable"];
step3:
$query = urldecode($_SERVER["QUERY_STRING"]);
if (preg_match("/ |_/", $query)) {
    echec();
}
if ($variable === "challengefox") {
    echo "- Si ce texte apparait, tu valides la premiere etape! <br />";
    if (isset($_GET["challenge_fox"])) {
        echo "- Deuxieme etape valide! <br />";
        if (hash("md2", $_GET["variable2"]) == "0") {
            echo "- Troisieme etape valide! <br />";
            if (hash("sha1", $_GET["variable3"]) == $_GET["variable3"]) {
                echo "- Okay, voici le flag : " . $secretflag . "<br />";
            }
        }
    }
}
source();

function source()
{
    echo "<br /><code>";
    highlight_string(file_get_contents(__FILE__));
    echo "</code>";
}

start:
include "flag.php";
echo "<title>Challenge Fox</title>";
echo "<b>Challenge Fox</b>";
echo "<p>Analyser le code ci dessous et trouver le moyen d afficher le flag.<p>";
echo "<br /><HR><br />";

```

## Step 2: Bypassing the First Check

The first check requires the `$variable` to be equal to "challengefox". However, there's a twist. The code uses `str_replace` to remove the string "challengefox" from the `$variable`.

**Solution:** To bypass this, we can introduce the string "chachallengefoxllengefox" in the `$variable`. This way, after the removal of the first occurrence, the second one remains intact. The parameter to be passed is: `variable=chachallengefoxllengefox`.

## Step 3: Bypassing the Underscore Filter

For the second step, the challenge is to set the `challenge_fox` parameter without using an underscore, as it's filtered out.

**Solution:** PHP interprets dots in GET parameter names as underscores. Thus, by setting the parameter as `challenge.fox`, it's internally interpreted as `challenge_fox`.

## Step 4 & 5: Exploiting Magic Hashes

The third and fourth steps involve comparing hashes. PHP has a known quirk with certain hash values, known as "magic hashes". When using loose comparison (`==`), these hashes can be interpreted as other values.

**Solution:**

1. For the third step, we need a string whose `md2` hash is equal to "0" when using loose comparison. The value `variable2=2HlFqrdIKK6z` produces an `md2` hash that, when compared loosely in PHP, is equal to "0".
    
2. For the fourth step, we exploit the `sha1` hash. The value `variable3=0e00000000000000000000081614617300000000` produces a `sha1` hash that, when compared loosely, is equal to itself. This is because any string of the form `0eX` where `X` is all numbers is considered as 0 in scientific notation in PHP.

## Final

Finally we get the flag : ESD{ChallengeFox486217935}
