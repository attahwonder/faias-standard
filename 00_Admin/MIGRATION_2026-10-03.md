# Migration map — FAIAS v1.3.1 file layout (3 October 2026)

**What moved.** Before v1.3.1 each domain's Review Canvases were held in one file, `V2_IRQ_Battery/canvases/CANVASES_<DOM>.md`, and each domain's test procedures in one file, `V3_Testing_Playbook/PLAYBOOK_<DOM>.md`. From v1.3.1 each canvas and each procedure is held in its own file beside the domain file, named `CANVASES_<DOM>_<nnn>.md` or `PLAYBOOK_<DOM>_<nnn>.md` by the number in its identifier. The domain file keeps its path and holds the domain's introductory text, a dated note listing the domain's files, and any closing text. `EXEMPLAR_CANVASES.md` and `PLAYBOOK_OVERVIEW.md` did not move.

**What did not change.** The text of each canvas and procedure, and of each domain file's introductory and closing text, is unchanged. The earlier files used CRLF line endings; the domain files and the canvas and procedure files of this release use LF line endings, and the text is otherwise byte for byte the same.

**How to read the tables.** For each earlier file, each row gives a range of its lines, the file that now holds them and the lines there. The new line number is the earlier line number minus the offset. A reference to an earlier file and line in a retained record resolves through these tables.

**Recovering a line's history.** Use `git log -S"<string>"` with no path, which finds the commit that wrote the string in the earlier file. Or use `git blame -C -C -C <new path>`, which names the earlier file and the last commit before this release, and then `git blame <that commit> -- <earlier path>`.

## V2_IRQ_Battery/canvases/CANVASES_AGT.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–19 | CANVASES_AGT.md | 1–19 | 0 |
| 20–215 | CANVASES_AGT_001.md | 1–196 | 19 |
| 216–405 | CANVASES_AGT_002.md | 1–190 | 215 |
| 406–609 | CANVASES_AGT_003.md | 1–204 | 405 |
| 610–807 | CANVASES_AGT_004.md | 1–198 | 609 |
| 808–1015 | CANVASES_AGT_005.md | 1–208 | 807 |
| 1016–1218 | CANVASES_AGT_006.md | 1–203 | 1015 |
| 1219–1421 | CANVASES_AGT_007.md | 1–203 | 1218 |
| 1422–1629 | CANVASES_AGT_008.md | 1–208 | 1421 |
| 1630–1845 | CANVASES_AGT_009.md | 1–216 | 1629 |
| 1846–2051 | CANVASES_AGT_010.md | 1–206 | 1845 |
| 2052–2269 | CANVASES_AGT_011.md | 1–218 | 2051 |
| 2270–2513 | CANVASES_AGT_012.md | 1–244 | 2269 |
| 2514–2722 | CANVASES_AGT_013.md | 1–209 | 2513 |
| 2723–3327 | CANVASES_AGT_014.md | 1–605 | 2722 |

## V2_IRQ_Battery/canvases/CANVASES_CON.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–16 | CANVASES_CON.md | 1–16 | 0 |
| 17–224 | CANVASES_CON_001.md | 1–208 | 16 |
| 225–407 | CANVASES_CON_002.md | 1–183 | 224 |
| 408–602 | CANVASES_CON_003.md | 1–195 | 407 |
| 603–802 | CANVASES_CON_004.md | 1–200 | 602 |
| 803–1014 | CANVASES_CON_005.md | 1–212 | 802 |
| 1015–1208 | CANVASES_CON_006.md | 1–194 | 1014 |
| 1209–1385 | CANVASES_CON_007.md | 1–177 | 1208 |
| 1386–1567 | CANVASES_CON_008.md | 1–182 | 1385 |
| 1568–1742 | CANVASES_CON_009.md | 1–175 | 1567 |
| 1743–2024 | CANVASES_CON_010.md | 1–282 | 1742 |

## V2_IRQ_Battery/canvases/CANVASES_DAT.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–16 | CANVASES_DAT.md | 1–16 | 0 |
| 17–189 | CANVASES_DAT_001.md | 1–173 | 16 |
| 190–368 | CANVASES_DAT_002.md | 1–179 | 189 |
| 369–532 | CANVASES_DAT_003.md | 1–164 | 368 |
| 533–705 | CANVASES_DAT_004.md | 1–173 | 532 |
| 706–878 | CANVASES_DAT_005.md | 1–173 | 705 |
| 879–1065 | CANVASES_DAT_006.md | 1–187 | 878 |
| 1066–1253 | CANVASES_DAT_013.md | 1–188 | 1065 |
| 1254–1431 | CANVASES_DAT_007.md | 1–178 | 1253 |
| 1432–1612 | CANVASES_DAT_008.md | 1–181 | 1431 |
| 1613–1795 | CANVASES_DAT_009.md | 1–183 | 1612 |
| 1796–1975 | CANVASES_DAT_010.md | 1–180 | 1795 |
| 1976–2162 | CANVASES_DAT_011.md | 1–187 | 1975 |
| 2163–2348 | CANVASES_DAT_012.md | 1–186 | 2162 |
| 2349–2558 | CANVASES_DAT_014.md | 1–210 | 2348 |
| 2559–2560 | CANVASES_DAT.md (closing text) | 40–41 | 2519 |

## V2_IRQ_Battery/canvases/CANVASES_GOV.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–11 | CANVASES_GOV.md | 1–11 | 0 |
| 12–195 | CANVASES_GOV_001.md | 1–184 | 11 |
| 196–391 | CANVASES_GOV_002.md | 1–196 | 195 |
| 392–586 | CANVASES_GOV_003.md | 1–195 | 391 |
| 587–786 | CANVASES_GOV_004.md | 1–200 | 586 |
| 787–983 | CANVASES_GOV_005.md | 1–197 | 786 |
| 984–1192 | CANVASES_GOV_006.md | 1–209 | 983 |
| 1193–1397 | CANVASES_GOV_007.md | 1–205 | 1192 |
| 1398–1599 | CANVASES_GOV_008.md | 1–202 | 1397 |
| 1600–1819 | CANVASES_GOV_009.md | 1–220 | 1599 |
| 1820–2040 | CANVASES_GOV_010.md | 1–221 | 1819 |
| 2041–2258 | CANVASES_GOV_011.md | 1–218 | 2040 |
| 2259–2536 | CANVASES_GOV_012.md | 1–278 | 2258 |
| 2537–2768 | CANVASES_GOV_013.md | 1–232 | 2536 |
| 2769–2999 | CANVASES_GOV_014.md | 1–231 | 2768 |
| 3000–3234 | CANVASES_GOV_015.md | 1–235 | 2999 |
| 3235–3459 | CANVASES_GOV_016.md | 1–225 | 3234 |
| 3460–3461 | CANVASES_GOV.md (closing text) | 35–36 | 3425 |

## V2_IRQ_Battery/canvases/CANVASES_HUM.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–19 | CANVASES_HUM.md | 1–19 | 0 |
| 20–241 | CANVASES_HUM_001.md | 1–222 | 19 |
| 242–458 | CANVASES_HUM_002.md | 1–217 | 241 |
| 459–672 | CANVASES_HUM_003.md | 1–214 | 458 |
| 673–892 | CANVASES_HUM_004.md | 1–220 | 672 |
| 893–1110 | CANVASES_HUM_005.md | 1–218 | 892 |
| 1111–1327 | CANVASES_HUM_006.md | 1–217 | 1110 |
| 1328–1548 | CANVASES_HUM_007.md | 1–221 | 1327 |
| 1549–1768 | CANVASES_HUM_008.md | 1–220 | 1548 |
| 1769–2012 | CANVASES_HUM_009.md | 1–244 | 1768 |

## V2_IRQ_Battery/canvases/CANVASES_MOD.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–21 | CANVASES_MOD.md | 1–21 | 0 |
| 22–211 | CANVASES_MOD_001.md | 1–190 | 21 |
| 212–408 | CANVASES_MOD_002.md | 1–197 | 211 |
| 409–599 | CANVASES_MOD_003.md | 1–191 | 408 |
| 600–812 | CANVASES_MOD_004.md | 1–213 | 599 |
| 813–1016 | CANVASES_MOD_005.md | 1–204 | 812 |
| 1017–1212 | CANVASES_MOD_007.md | 1–196 | 1016 |
| 1213–1426 | CANVASES_MOD_008.md | 1–214 | 1212 |
| 1427–1639 | CANVASES_MOD_009.md | 1–213 | 1426 |
| 1640–1856 | CANVASES_MOD_010.md | 1–217 | 1639 |
| 1857–2074 | CANVASES_MOD_011.md | 1–218 | 1856 |
| 2075–2289 | CANVASES_MOD_012.md | 1–215 | 2074 |
| 2290–2494 | CANVASES_MOD_013.md | 1–205 | 2289 |
| 2495–2691 | CANVASES_MOD_014.md | 1–197 | 2494 |
| 2692–2910 | CANVASES_MOD_015.md | 1–219 | 2691 |
| 2911–3293 | CANVASES_MOD_016.md | 1–383 | 2910 |
| 3294–3297 | CANVASES_MOD.md (closing text) | 44–47 | 3250 |

## V2_IRQ_Battery/canvases/CANVASES_RES.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–16 | CANVASES_RES.md | 1–16 | 0 |
| 17–199 | CANVASES_RES_001.md | 1–183 | 16 |
| 200–377 | CANVASES_RES_002.md | 1–178 | 199 |
| 378–556 | CANVASES_RES_003.md | 1–179 | 377 |
| 557–765 | CANVASES_RES_004.md | 1–209 | 556 |
| 766–950 | CANVASES_RES_005.md | 1–185 | 765 |
| 951–1163 | CANVASES_RES_006.md | 1–213 | 950 |
| 1164–1355 | CANVASES_RES_007.md | 1–192 | 1163 |

## V2_IRQ_Battery/canvases/CANVASES_SEC.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–18 | CANVASES_SEC.md | 1–18 | 0 |
| 19–227 | CANVASES_SEC_001.md | 1–209 | 18 |
| 228–414 | CANVASES_SEC_002.md | 1–187 | 227 |
| 415–632 | CANVASES_SEC_004.md | 1–218 | 414 |
| 633–826 | CANVASES_SEC_005.md | 1–194 | 632 |
| 827–1014 | CANVASES_SEC_006.md | 1–188 | 826 |
| 1015–1220 | CANVASES_SEC_007.md | 1–206 | 1014 |
| 1221–1413 | CANVASES_SEC_008.md | 1–193 | 1220 |
| 1414–1613 | CANVASES_SEC_009.md | 1–200 | 1413 |
| 1614–1825 | CANVASES_SEC_010.md | 1–212 | 1613 |
| 1826–2042 | CANVASES_SEC_011.md | 1–217 | 1825 |
| 2043–2258 | CANVASES_SEC_012.md | 1–216 | 2042 |
| 2259–2500 | CANVASES_SEC_013.md | 1–242 | 2258 |
| 2501–2720 | CANVASES_SEC_014.md | 1–220 | 2500 |

## V2_IRQ_Battery/canvases/CANVASES_TPR.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–16 | CANVASES_TPR.md | 1–16 | 0 |
| 17–200 | CANVASES_TPR_001.md | 1–184 | 16 |
| 201–376 | CANVASES_TPR_002.md | 1–176 | 200 |
| 377–549 | CANVASES_TPR_003.md | 1–173 | 376 |
| 550–732 | CANVASES_TPR_004.md | 1–183 | 549 |
| 733–901 | CANVASES_TPR_005.md | 1–169 | 732 |
| 902–1071 | CANVASES_TPR_006.md | 1–170 | 901 |
| 1072–1247 | CANVASES_TPR_007.md | 1–176 | 1071 |
| 1248–1435 | CANVASES_TPR_008.md | 1–188 | 1247 |
| 1436–1608 | CANVASES_TPR_009.md | 1–173 | 1435 |

## V3_Testing_Playbook/PLAYBOOK_AGT.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–93 | PLAYBOOK_AGT.md | 1–93 | 0 |
| 94–183 | PLAYBOOK_AGT_001.md | 1–90 | 93 |
| 184–268 | PLAYBOOK_AGT_002.md | 1–85 | 183 |
| 269–353 | PLAYBOOK_AGT_003.md | 1–85 | 268 |
| 354–444 | PLAYBOOK_AGT_004.md | 1–91 | 353 |
| 445–531 | PLAYBOOK_AGT_005.md | 1–87 | 444 |
| 532–612 | PLAYBOOK_AGT_006.md | 1–81 | 531 |
| 613–702 | PLAYBOOK_AGT_007.md | 1–90 | 612 |
| 703–793 | PLAYBOOK_AGT_008.md | 1–91 | 702 |
| 794–879 | PLAYBOOK_AGT_009.md | 1–86 | 793 |
| 880–968 | PLAYBOOK_AGT_010.md | 1–89 | 879 |
| 969–1058 | PLAYBOOK_AGT_011.md | 1–90 | 968 |
| 1059–1147 | PLAYBOOK_AGT_012.md | 1–89 | 1058 |
| 1148–1238 | PLAYBOOK_AGT_013.md | 1–91 | 1147 |
| 1239–1321 | PLAYBOOK_AGT_014.md | 1–83 | 1238 |
| 1322–1356 | PLAYBOOK_AGT.md (closing text) | 115–149 | 1207 |

## V3_Testing_Playbook/PLAYBOOK_CON.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–28 | PLAYBOOK_CON.md | 1–28 | 0 |
| 29–108 | PLAYBOOK_CON_001.md | 1–80 | 28 |
| 109–185 | PLAYBOOK_CON_002.md | 1–77 | 108 |
| 186–266 | PLAYBOOK_CON_003.md | 1–81 | 185 |
| 267–346 | PLAYBOOK_CON_004.md | 1–80 | 266 |
| 347–426 | PLAYBOOK_CON_005.md | 1–80 | 346 |
| 427–503 | PLAYBOOK_CON_006.md | 1–77 | 426 |
| 504–583 | PLAYBOOK_CON_007.md | 1–80 | 503 |
| 584–665 | PLAYBOOK_CON_008.md | 1–82 | 583 |
| 666–768 | PLAYBOOK_CON_009.md | 1–103 | 665 |
| 769–862 | PLAYBOOK_CON_010.md | 1–94 | 768 |
| 863–893 | PLAYBOOK_CON.md (closing text) | 46–76 | 817 |

## V3_Testing_Playbook/PLAYBOOK_DAT.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–79 | PLAYBOOK_DAT.md | 1–79 | 0 |
| 80–156 | PLAYBOOK_DAT_001.md | 1–77 | 79 |
| 157–238 | PLAYBOOK_DAT_002.md | 1–82 | 156 |
| 239–318 | PLAYBOOK_DAT_003.md | 1–80 | 238 |
| 319–396 | PLAYBOOK_DAT_004.md | 1–78 | 318 |
| 397–474 | PLAYBOOK_DAT_005.md | 1–78 | 396 |
| 475–559 | PLAYBOOK_DAT_006.md | 1–85 | 474 |
| 560–640 | PLAYBOOK_DAT_007.md | 1–81 | 559 |
| 641–719 | PLAYBOOK_DAT_008.md | 1–79 | 640 |
| 720–804 | PLAYBOOK_DAT_009.md | 1–85 | 719 |
| 805–886 | PLAYBOOK_DAT_010.md | 1–82 | 804 |
| 887–970 | PLAYBOOK_DAT_011.md | 1–84 | 886 |
| 971–1054 | PLAYBOOK_DAT_012.md | 1–84 | 970 |
| 1055–1137 | PLAYBOOK_DAT_013.md | 1–83 | 1054 |
| 1138–1223 | PLAYBOOK_DAT_014.md | 1–86 | 1137 |
| 1224–1255 | PLAYBOOK_DAT.md (closing text) | 101–132 | 1123 |

## V3_Testing_Playbook/PLAYBOOK_GOV.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–27 | PLAYBOOK_GOV.md | 1–27 | 0 |
| 28–105 | PLAYBOOK_GOV_001.md | 1–78 | 27 |
| 106–182 | PLAYBOOK_GOV_002.md | 1–77 | 105 |
| 183–260 | PLAYBOOK_GOV_003.md | 1–78 | 182 |
| 261–335 | PLAYBOOK_GOV_004.md | 1–75 | 260 |
| 336–412 | PLAYBOOK_GOV_005.md | 1–77 | 335 |
| 413–488 | PLAYBOOK_GOV_006.md | 1–76 | 412 |
| 489–568 | PLAYBOOK_GOV_007.md | 1–80 | 488 |
| 569–645 | PLAYBOOK_GOV_008.md | 1–77 | 568 |
| 646–727 | PLAYBOOK_GOV_009.md | 1–82 | 645 |
| 728–810 | PLAYBOOK_GOV_010.md | 1–83 | 727 |
| 811–892 | PLAYBOOK_GOV_011.md | 1–82 | 810 |
| 893–985 | PLAYBOOK_GOV_012.md | 1–93 | 892 |
| 986–1080 | PLAYBOOK_GOV_013.md | 1–95 | 985 |
| 1081–1173 | PLAYBOOK_GOV_014.md | 1–93 | 1080 |
| 1174–1267 | PLAYBOOK_GOV_015.md | 1–94 | 1173 |
| 1268–1361 | PLAYBOOK_GOV_016.md | 1–94 | 1267 |
| 1362–1401 | PLAYBOOK_GOV.md (closing text) | 51–90 | 1311 |

## V3_Testing_Playbook/PLAYBOOK_HUM.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–64 | PLAYBOOK_HUM.md | 1–64 | 0 |
| 65–149 | PLAYBOOK_HUM_001.md | 1–85 | 64 |
| 150–226 | PLAYBOOK_HUM_002.md | 1–77 | 149 |
| 227–313 | PLAYBOOK_HUM_003.md | 1–87 | 226 |
| 314–391 | PLAYBOOK_HUM_004.md | 1–78 | 313 |
| 392–479 | PLAYBOOK_HUM_005.md | 1–88 | 391 |
| 480–564 | PLAYBOOK_HUM_006.md | 1–85 | 479 |
| 565–661 | PLAYBOOK_HUM_007.md | 1–97 | 564 |
| 662–749 | PLAYBOOK_HUM_008.md | 1–88 | 661 |
| 750–834 | PLAYBOOK_HUM_009.md | 1–85 | 749 |
| 835–862 | PLAYBOOK_HUM.md (closing text) | 81–108 | 754 |

## V3_Testing_Playbook/PLAYBOOK_MOD.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–76 | PLAYBOOK_MOD.md | 1–76 | 0 |
| 77–159 | PLAYBOOK_MOD_001.md | 1–83 | 76 |
| 160–244 | PLAYBOOK_MOD_002.md | 1–85 | 159 |
| 245–327 | PLAYBOOK_MOD_003.md | 1–83 | 244 |
| 328–412 | PLAYBOOK_MOD_004.md | 1–85 | 327 |
| 413–500 | PLAYBOOK_MOD_005.md | 1–88 | 412 |
| 501–591 | PLAYBOOK_MOD_006.md | 1–91 | 500 |
| 592–674 | PLAYBOOK_MOD_007.md | 1–83 | 591 |
| 675–760 | PLAYBOOK_MOD_008.md | 1–86 | 674 |
| 761–847 | PLAYBOOK_MOD_009.md | 1–87 | 760 |
| 848–942 | PLAYBOOK_MOD_010.md | 1–95 | 847 |
| 943–1025 | PLAYBOOK_MOD_011.md | 1–83 | 942 |
| 1026–1112 | PLAYBOOK_MOD_012.md | 1–87 | 1025 |
| 1113–1196 | PLAYBOOK_MOD_013.md | 1–84 | 1112 |
| 1197–1287 | PLAYBOOK_MOD_014.md | 1–91 | 1196 |
| 1288–1383 | PLAYBOOK_MOD_015.md | 1–96 | 1287 |
| 1384–1489 | PLAYBOOK_MOD_016.md | 1–106 | 1383 |
| 1490–1523 | PLAYBOOK_MOD.md (closing text) | 100–133 | 1390 |

## V3_Testing_Playbook/PLAYBOOK_RES.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–25 | PLAYBOOK_RES.md | 1–25 | 0 |
| 26–102 | PLAYBOOK_RES_001.md | 1–77 | 25 |
| 103–178 | PLAYBOOK_RES_002.md | 1–76 | 102 |
| 179–249 | PLAYBOOK_RES_003.md | 1–71 | 178 |
| 250–324 | PLAYBOOK_RES_004.md | 1–75 | 249 |
| 325–396 | PLAYBOOK_RES_005.md | 1–72 | 324 |
| 397–473 | PLAYBOOK_RES_006.md | 1–77 | 396 |
| 474–545 | PLAYBOOK_RES_007.md | 1–72 | 473 |
| 546–573 | PLAYBOOK_RES.md (closing text) | 40–67 | 506 |

## V3_Testing_Playbook/PLAYBOOK_SEC.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–62 | PLAYBOOK_SEC.md | 1–62 | 0 |
| 63–140 | PLAYBOOK_SEC_001.md | 1–78 | 62 |
| 141–212 | PLAYBOOK_SEC_002.md | 1–72 | 140 |
| 213–296 | PLAYBOOK_SEC_003.md | 1–84 | 212 |
| 297–384 | PLAYBOOK_SEC_004.md | 1–88 | 296 |
| 385–464 | PLAYBOOK_SEC_005.md | 1–80 | 384 |
| 465–545 | PLAYBOOK_SEC_006.md | 1–81 | 464 |
| 546–623 | PLAYBOOK_SEC_007.md | 1–78 | 545 |
| 624–704 | PLAYBOOK_SEC_008.md | 1–81 | 623 |
| 705–782 | PLAYBOOK_SEC_009.md | 1–78 | 704 |
| 783–857 | PLAYBOOK_SEC_010.md | 1–75 | 782 |
| 858–935 | PLAYBOOK_SEC_011.md | 1–78 | 857 |
| 936–1019 | PLAYBOOK_SEC_012.md | 1–84 | 935 |
| 1020–1111 | PLAYBOOK_SEC_013.md | 1–92 | 1019 |
| 1112–1196 | PLAYBOOK_SEC_014.md | 1–85 | 1111 |
| 1197–1227 | PLAYBOOK_SEC.md (closing text) | 84–114 | 1113 |

## V3_Testing_Playbook/PLAYBOOK_TPR.md

| Earlier lines | Now in | Lines there | Offset |
|---|---|---|---|
| 1–61 | PLAYBOOK_TPR.md | 1–61 | 0 |
| 62–140 | PLAYBOOK_TPR_001.md | 1–79 | 61 |
| 141–224 | PLAYBOOK_TPR_002.md | 1–84 | 140 |
| 225–306 | PLAYBOOK_TPR_003.md | 1–82 | 224 |
| 307–391 | PLAYBOOK_TPR_004.md | 1–85 | 306 |
| 392–476 | PLAYBOOK_TPR_005.md | 1–85 | 391 |
| 477–560 | PLAYBOOK_TPR_006.md | 1–84 | 476 |
| 561–641 | PLAYBOOK_TPR_007.md | 1–81 | 560 |
| 642–726 | PLAYBOOK_TPR_008.md | 1–85 | 641 |
| 727–811 | PLAYBOOK_TPR_009.md | 1–85 | 726 |
| 812–836 | PLAYBOOK_TPR.md (closing text) | 78–102 | 734 |
