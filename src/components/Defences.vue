<template>
  <div class="defence-stats d-flex justify-content-center">
    <table class="stat-sheet">
      <tbody>
        <tr class="tr-head">
          <td>Physical Def</td>
          <td>
            <input type="text" readonly v-model="physicalDefence.physical">
          </td>
        </tr>
        <tr class="tr-subhead">
          <td>
            VS strike
          </td>
          <td>
            <input type="text" readonly v-model="physicalDefence.strike">
          </td>
        </tr>
        <tr class="tr-subhead">
          <td>
            VS slash
          </td>
          <td>
            <input type="text" readonly v-model="physicalDefence.slash">
          </td>
        </tr>
        <tr class="tr-subhead">
          <td>
            VS thrust
          </td>
          <td>
            <input type="text" readonly v-model="physicalDefence.thrust">
          </td>
        </tr>
        <tr class="tr-head">
          <td>Magic Def</td>
          <td>
            <input type="text" readonly v-model="elementalDefence.magic">
          </td>
        </tr>
        <tr class="tr-head">
          <td>Flame Def</td>
          <td>
            <input type="text" readonly v-model="elementalDefence.fire">
          </td>
        </tr>
        <tr class="tr-head">
          <td>Lightning Def</td>
          <td>
            <input type="text" readonly v-model="elementalDefence.lightning">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'defence-stats',
  props: {
    characterStats: {
      type: Object,
      required: true,
    },
  },
  data: () => ({
    physicalDefence: {
      physical: 0,
      phsyicalBase: 0,
      strike: 0,
      slash: 0,
      thrust : 0
    },
    elementalDefence: {
      magic: 0,
      fire: 0,
      lightning: 0
    },
    statSum : 0,
    characterResistanceStat: 0,
    characterFaithStat: 0,
    physicalDefenceTable: {
      82 : 12, 83 : 13, 84 : 14, 85 : 16, 86 : 17, 87 : 18, 88 : 20, 89 : 21, 90 : 22, 91 : 24, 92 : 25, 93 : 26, 94 : 28, 95 : 29, 96 : 30, 97 : 32, 98 : 33, 99 : 34, 100 : 36, 101 : 37, 102 : 38, 103 : 40, 104 : 41, 105 : 42, 106 : 44, 107 : 45, 108 : 46, 109 : 48, 110 : 49, 111 : 50, 112 : 52, 113 : 53, 114 : 54, 115 : 55, 116 : 57, 117 : 58, 118 : 59, 119 : 61, 120 : 62, 121 : 63, 122 : 64, 123 : 66, 124 : 67, 125 : 68, 126 : 70, 127 : 71, 128 : 72, 129 : 73, 130 : 75, 131 : 76, 132 : 77, 133 : 78, 134 : 80, 135 : 81, 136 : 82, 137 : 83, 138 : 85, 139 : 86, 140 : 87, 141 : 88, 142 : 89, 143 : 91, 144 : 92, 145 : 93, 146 : 94, 147 : 95, 148 : 97, 149 : 98, 150 : 99, 151 : 100, 152 : 101, 153 : 102, 154 : 104, 155 : 105, 156 : 106, 157 : 107, 158 : 108, 159 : 109, 160 : 110, 161 : 111, 162 : 112, 163 : 114, 164 : 115, 165 : 116, 166 : 117, 167 : 118, 168 : 119, 169 : 119, 170 : 120, 171 : 121, 172 : 121, 173 : 122, 174 : 122, 175 : 123, 176 : 123, 177 : 124, 178 : 124, 179 : 125, 180 : 125, 181 : 126, 182 : 127, 183 : 127, 184 : 128, 185 : 128, 186 : 129, 187 : 129, 188 : 130, 189 : 130, 190 : 131, 191 : 131, 192 : 132, 193 : 132, 194 : 133, 195 : 133, 196 : 134, 197 : 134, 198 : 135, 199 : 135, 200 : 136, 201 : 136, 202 : 137, 203 : 137, 204 : 138, 205 : 138, 206 : 139, 207 : 139, 208 : 140, 209 : 140, 210 : 141, 211 : 141, 212 : 142, 213 : 142, 214 : 143, 215 : 143, 216 : 144, 217 : 144, 218 : 145, 219 : 145, 220 : 146, 221 : 146, 222 : 147, 223 : 147, 224 : 148, 225 : 148, 226 : 149, 227 : 149, 228 : 149, 229 : 150, 230 : 150, 231 : 151, 232 : 151, 233 : 152, 234 : 152, 235 : 153, 236 : 153, 237 : 154, 238 : 154, 239 : 154, 240 : 155, 241 : 155, 242 : 156, 243 : 156, 244 : 157, 245 : 157, 246 : 158, 247 : 158, 248 : 158, 249 : 159, 250 : 159, 251 : 160, 252 : 160, 253 : 160, 254 : 161, 255 : 161, 256 : 162, 257 : 162, 258 : 162, 259 : 163, 260 : 163, 261 : 164, 262 : 164
    },
    physicalDefence99Table: {
      171 : 164, 172 : 164, 173 : 165, 174 : 165, 175 : 166, 176 : 166, 177 : 166, 178 : 167, 179 : 167, 180 : 167, 181 : 168, 182 : 168, 183 : 168, 184 : 169, 185 : 169, 186 : 169, 187 : 169, 188 : 170, 189 : 170, 190 : 170, 191 : 170, 192 : 170, 193 : 170, 194 : 170, 195 : 170, 196 : 170, 197 : 170, 198 : 170, 199 : 170, 200 : 171, 201 : 171, 202 : 171, 203 : 171, 204 : 171, 205 : 171, 206 : 171, 207 : 171, 208 : 171, 209 : 171, 210 : 171, 211 : 171, 212 : 171, 213 : 171, 214 : 171, 215 : 171, 216 : 171, 217 : 171, 218 : 171, 219 : 171, 220 : 172, 221 : 172, 222 : 172, 223 : 172, 224 : 172, 225 : 172, 226 : 172, 227 : 172, 228 : 172, 229 : 172, 230 : 172, 231 : 172, 232 : 172, 233 : 172, 234 : 172, 235 : 172, 236 : 172, 237 : 172, 238 : 172, 239 : 172, 240 : 173, 241 : 173, 242 : 173, 243 : 173, 244 : 173, 245 : 173, 246 : 173, 247 : 173, 248 : 173, 249 : 173, 250 : 173, 251 : 173, 252 : 173, 253 : 173, 254 : 173, 255 : 173, 256 : 173, 257 : 173, 258 : 173, 259 : 173, 260 : 174, 261 : 174, 262 : 174, 263 : 174, 264 : 174, 265 : 174, 266 : 174, 267 : 174, 268 : 174, 269 : 174, 270 : 174, 271 : 174, 272 : 174, 273 : 174, 274 : 174, 275 : 174, 276 : 174, 277 : 174, 278 : 174, 279 : 174, 280 : 175, 281 : 175, 282 : 175, 283 : 175, 284 : 175, 285 : 175, 286 : 175, 287 : 175, 288 : 175, 289 : 175, 290 : 175, 291 : 175, 292 : 175, 293 : 175, 294 : 175, 295 : 175, 296 : 175, 297 : 175, 298 : 175, 299 : 175, 300 : 176, 301 : 176, 302 : 176, 303 : 176, 304 : 176, 305 : 176, 306 : 176, 307 : 176, 308 : 176, 309 : 176, 310 : 176, 311 : 176, 312 : 176, 313 : 176, 314 : 176, 315 : 176, 316 : 176, 317 : 176, 318 : 176, 319 : 176, 320 : 177, 321 : 177, 322 : 177, 323 : 177, 324 : 177, 325 : 177, 326 : 177, 327 : 177, 328 : 177, 329 : 177, 330 : 177, 331 : 177, 332 : 177, 333 : 177, 334 : 177, 335 : 177, 336 : 177, 337 : 177, 338 : 177, 339 : 177, 340 : 178, 341 : 178, 342 : 178, 343 : 178, 344 : 178, 345 : 178, 346 : 178, 347 : 178, 348 : 178, 349 : 178, 350 : 178, 351 : 178, 352 : 178, 353 : 178, 354 : 178, 355 : 178, 356 : 178, 357 : 178, 358 : 178, 359 : 178, 360 : 179, 361 : 179, 362 : 179, 363 : 179, 364 : 179, 365 : 179, 366 : 179, 367 : 179, 368 : 179, 369 : 179, 370 : 179, 371 : 179, 372 : 179, 373 : 179, 374 : 179, 375 : 179, 376 : 179, 377 : 179, 378 : 179, 379 : 179, 380 : 180, 381 : 180, 382 : 180, 383 : 180, 384 : 180, 385 : 180, 386 : 180, 387 : 180, 388 : 180, 389 : 180, 390 : 180, 391 : 180, 392 : 180, 393 : 180, 394 : 180, 395 : 180, 396 : 180, 397 : 180, 398 : 180, 399 : 180, 400 : 181, 401 : 181, 402 : 181, 403 : 181, 404 : 181, 405 : 181, 406 : 181, 407 : 181, 408 : 181, 409 : 181, 410 : 181, 411 : 181, 412 : 181, 413 : 181, 414 : 181, 415 : 181, 416 : 181, 417 : 181, 418 : 181, 419 : 181, 420 : 182, 421 : 182, 422 : 182, 423 : 182, 424 : 182, 425 : 182, 426 : 182, 427 : 182, 428 : 182, 429 : 182, 430 : 182, 431 : 182, 432 : 182, 433 : 182, 434 : 182, 435 : 182, 436 : 182, 437 : 182, 438 : 182, 439 : 182, 440 : 183, 441 : 183, 442 : 183, 443 : 183, 444 : 183, 445 : 183, 446 : 183, 447 : 183, 448 : 183, 449 : 183, 450 : 183, 451 : 183, 452 : 183, 453 : 183, 454 : 183, 455 : 183, 456 : 183, 457 : 183, 458 : 183, 459 : 183, 460 : 184, 461 : 184, 462 : 184, 463 : 184, 464 : 184, 465 : 184, 466 : 184, 467 : 184, 468 : 184, 469 : 184, 470 : 184, 471 : 184, 472 : 184, 473 : 184, 474 : 184, 475 : 184, 476 : 184, 477 : 184, 478 : 184, 479 : 184, 480 : 185, 481 : 185, 482 : 185, 483 : 185, 484 : 185, 485 : 185, 486 : 185, 487 : 185, 488 : 185, 489 : 185, 490 : 185, 491 : 185, 492 : 185, 493 : 185, 494 : 185, 495 : 185, 496 : 185, 497 : 185, 498 : 185, 499 : 185, 500 : 186, 501 : 186, 502 : 186, 503 : 186, 504 : 186, 505 : 186, 506 : 186, 507 : 186, 508 : 186, 509 : 186, 510 : 186, 511 : 186, 512 : 186, 513 : 186, 514 : 186, 515 : 186, 516 : 186, 517 : 186, 518 : 186, 519 : 186, 520 : 187, 521 : 187, 522 : 187, 523 : 187, 524 : 187, 525 : 187, 526 : 187, 527 : 187, 528 : 187, 529 : 187, 530 : 187, 531 : 187, 532 : 187, 533 : 187, 534 : 187, 535 : 187, 536 : 187, 537 : 187, 538 : 187, 539 : 187, 540 : 188, 541 : 188, 542 : 188, 543 : 188, 544 : 188, 545 : 188, 546 : 188, 547 : 188, 548 : 188, 549 : 188, 550 : 188, 551 : 188, 552 : 188, 553 : 188, 554 : 188, 555 : 188, 556 : 188, 557 : 188, 558 : 188, 559 : 188, 560 : 189, 561 : 189, 562 : 189, 563 : 189, 564 : 189, 565 : 189, 566 : 189, 567 : 189, 568 : 189, 569 : 189, 570 : 189, 571 : 189, 572 : 189, 573 : 189, 574 : 189, 575 : 189, 576 : 189, 577 : 189, 578 : 189, 579 : 189, 580 : 190, 581 : 190, 582 : 190, 583 : 190, 584 : 190, 585 : 190, 586 : 190, 587 : 190, 588 : 190, 589 : 190, 590 : 190, 591 : 190, 592 : 190, 593 : 190, 594 : 190, 595 : 190, 596 : 190, 597 : 190, 598 : 190, 599 : 190, 600 : 191, 601 : 191, 602 : 191, 603 : 191, 604 : 191, 605 : 191, 606 : 191, 607 : 191, 608 : 191, 609 : 191, 610 : 191, 611 : 191, 612 : 191, 613 : 191, 614 : 191, 615 : 191, 616 : 191, 617 : 191, 618 : 191, 619 : 191, 620 : 192, 621 : 192, 622 : 192, 623 : 192, 624 : 192, 625 : 192, 626 : 192, 627 : 192, 628 : 192, 629 : 192, 630 : 192, 631 : 192, 632 : 192, 633 : 192, 634 : 192, 635 : 192, 636 : 192, 637 : 192, 638 : 192, 639 : 192, 640 : 193, 641 : 193, 642 : 193, 643 : 193, 644 : 193, 645 : 193, 646 : 193, 647 : 193, 648 : 193, 649 : 193, 650 : 193, 651 : 193, 652 : 193, 653 : 193, 654 : 193, 655 : 193, 656 : 193, 657 : 193, 658 : 193, 659 : 193, 660 : 194, 661 : 194, 662 : 194, 663 : 194, 664 : 194, 665 : 194, 666 : 194, 667 : 194, 668 : 194, 669 : 194, 670 : 194, 671 : 194, 672 : 194, 673 : 194, 674 : 194, 675 : 194, 676 : 194, 677 : 194, 678 : 194, 679 : 194, 680 : 195, 681 : 195, 682 : 195, 683 : 195, 684 : 195, 685 : 195, 686 : 195, 687 : 195, 688 : 195, 689 : 195, 690 : 195, 691 : 195, 692 : 195, 693 : 195, 694 : 195, 695 : 195, 696 : 195, 697 : 195, 698 : 195, 699 : 195, 700 : 196, 701 : 196, 702 : 196, 703 : 196, 704 : 196, 705 : 196, 706 : 196, 707 : 196, 708 : 196, 709 : 196, 710 : 196, 711 : 196, 712 : 196, 713 : 196, 714 : 196, 715 : 196, 716 : 196, 717 : 196, 718 : 196, 719 : 196, 720 : 197, 721 : 197, 722 : 197, 723 : 197, 724 : 197, 725 : 197, 726 : 197, 727 : 197, 728 : 197, 729 : 197, 730 : 197, 731 : 197, 732 : 197, 733 : 197, 734 : 197, 735 : 197, 736 : 197, 737 : 197, 738 : 197, 739 : 197, 740 : 198, 741 : 198, 742 : 198, 743 : 198, 744 : 198, 745 : 198, 746 : 198, 747 : 198, 748 : 198, 749 : 198, 750 : 198, 751 : 198, 752 : 198, 753 : 198, 754 : 198, 755 : 198, 756 : 198, 757 : 198, 758 : 198, 759 : 198, 760 : 199, 761 : 199, 762 : 199, 763 : 199, 764 : 199, 765 : 199, 766 : 199, 767 : 199, 768 : 199, 769 : 199, 770 : 199, 771 : 199, 772 : 199, 773 : 199, 774 : 199, 775 : 199, 776 : 199, 777 : 199, 778 : 199, 779 : 199, 780 : 200, 781 : 200, 782 : 200, 783 : 200, 784 : 200, 785 : 200, 786 : 200, 787 : 200, 788 : 200, 789 : 200, 790 : 200, 791 : 200, 792 : 200,
    },
    magFireDefenceTable: {
      82 : 11, 83 : 12, 84 : 13, 85 : 15, 86 : 16, 87 : 17, 88 : 18, 89 : 20, 90 : 21, 91 : 22, 92 : 24, 93 : 25, 94 : 26, 95 : 27, 96 : 29, 97 : 30, 98 : 31, 99 : 32, 100 : 34, 101 : 35, 102 : 36, 103 : 37, 104 : 39, 105 : 40, 106 : 41, 107 : 42, 108 : 44, 109 : 45, 110 : 46, 111 : 47, 112 : 49, 113 : 50, 114 : 51, 115 : 52, 116 : 54, 117 : 55, 118 : 56, 119 : 57, 120 : 58, 121 : 60, 122 : 61, 123 : 62, 124 : 63, 125 : 65, 126 : 66, 127 : 67, 128 : 68, 129 : 69, 130 : 71, 131 : 72, 132 : 73, 133 : 74, 134 : 75, 135 : 76, 136 : 78, 137 : 79, 138 : 80, 139 : 81, 140 : 82, 141 : 83, 142 : 85, 143 : 86, 144 : 87, 145 : 88, 146 : 89, 147 : 90, 148 : 92, 149 : 93, 150 : 94, 151 : 95, 152 : 96, 153 : 97, 154 : 98, 155 : 99, 156 : 100, 157 : 102, 158 : 103, 159 : 104, 160 : 105, 161 : 106, 162 : 107, 163 : 108, 164 : 109, 165 : 110, 166 : 111, 167 : 112, 168 : 113, 169 : 114, 170 : 115, 171 : 116, 172 : 117, 173 : 118, 174 : 119, 175 : 120, 176 : 120, 177 : 121, 178 : 121, 179 : 122, 180 : 122, 181 : 123, 182 : 123, 183 : 124, 184 : 124, 185 : 125, 186 : 125, 187 : 126, 188 : 126, 189 : 127, 190 : 127, 191 : 128, 192 : 128, 193 : 129, 194 : 129, 195 : 130, 196 : 130, 197 : 131, 198 : 131, 199 : 132, 200 : 132, 201 : 133, 202 : 133, 203 : 134, 204 : 134, 205 : 135, 206 : 135, 207 : 136, 208 : 136, 209 : 137, 210 : 137, 211 : 137, 212 : 138, 213 : 138, 214 : 139, 215 : 139, 216 : 140, 217 : 140, 218 : 141, 219 : 141, 220 : 142, 221 : 142, 222 : 143, 223 : 143, 224 : 144, 225 : 144, 226 : 144, 227 : 145, 228 : 145, 229 : 146, 230 : 146, 231 : 147, 232 : 147, 233 : 148, 234 : 148, 235 : 149, 236 : 149, 237 : 149, 238 : 150, 239 : 150, 240 : 151, 241 : 151, 242 : 152, 243 : 152, 244 : 152, 245 : 153, 246 : 153, 247 : 154, 248 : 154, 249 : 155, 250 : 155, 251 : 155, 252 : 156, 253 : 156, 254 : 157, 255 : 157, 256 : 157, 257 : 158, 258 : 158, 259 : 159, 260 : 159, 261 : 159, 262 : 160, 263 : 160, 264 : 161, 265 : 161, 266 : 161, 267 : 162, 268 : 162, 269 : 163, 270 : 163, 271 : 163, 272 : 164, 273 : 164, 274 : 164, 275 : 165, 276 : 165, 277 : 165, 278 : 166, 279 : 166, 280 : 166, 281 : 167, 282 : 167, 283 : 167, 284 : 168, 285 : 168, 286 : 168, 287 : 169, 288 : 169, 289 : 169, 290 : 169, 291 : 170, 292 : 170, 293 : 170, 294 : 170, 295 : 170, 296 : 170, 297 : 170, 298 : 170, 299 : 170, 300 : 170, 301 : 170, 302 : 170, 303 : 170, 304 : 171, 305 : 171, 306 : 171, 307 : 171, 308 : 171, 309 : 171, 310 : 171, 311 : 171, 312 : 171, 313 : 171, 314 : 171, 315 : 171, 316 : 171, 317 : 171, 318 : 171, 319 : 171, 320 : 171, 321 : 171, 322 : 171, 323 : 171, 324 : 171, 325 : 172,
    },
    magFireDefence99Table: {
      181 : 172, 182 : 172, 183 : 172, 184 : 172, 185 : 172, 186 : 172, 187 : 172, 188 : 172, 189 : 172, 190 : 172, 191 : 172, 192 : 172, 193 : 172, 194 : 172, 195 : 172, 196 : 172, 197 : 172, 198 : 172, 199 : 172, 200 : 172, 201 : 172, 202 : 173, 203 : 173, 204 : 173, 205 : 173, 206 : 173, 207 : 173, 208 : 173, 209 : 173, 210 : 173, 211 : 173, 212 : 173, 213 : 173, 214 : 173, 215 : 173, 216 : 173, 217 : 173, 218 : 173, 219 : 173, 220 : 173, 221 : 173, 222 : 173, 223 : 174, 224 : 174, 225 : 174, 226 : 174, 227 : 174, 228 : 174, 229 : 174, 230 : 174, 231 : 174, 232 : 174, 233 : 174, 234 : 174, 235 : 174, 236 : 174, 237 : 174, 238 : 174, 239 : 174, 240 : 174, 241 : 174, 242 : 174, 243 : 174, 244 : 175, 245 : 175, 246 : 175, 247 : 175, 248 : 175, 249 : 175, 250 : 175, 251 : 175, 252 : 175, 253 : 175, 254 : 175, 255 : 175, 256 : 175, 257 : 175, 258 : 175, 259 : 175, 260 : 175, 261 : 175, 262 : 175, 263 : 175, 264 : 175, 265 : 175, 266 : 176, 267 : 176, 268 : 176, 269 : 176, 270 : 176, 271 : 176, 272 : 176, 273 : 176, 274 : 176, 275 : 176, 276 : 176, 277 : 176, 278 : 176, 279 : 176, 280 : 176, 281 : 176, 282 : 176, 283 : 176, 284 : 176, 285 : 176, 286 : 176, 287 : 177, 288 : 177, 289 : 177, 290 : 177, 291 : 177, 292 : 177, 293 : 177, 294 : 177, 295 : 177, 296 : 177, 297 : 177, 298 : 177, 299 : 177, 300 : 177, 301 : 177, 302 : 177, 303 : 177, 304 : 177, 305 : 177, 306 : 177, 307 : 177, 308 : 178, 309 : 178, 310 : 178, 311 : 178, 312 : 178, 313 : 178, 314 : 178, 315 : 178, 316 : 178, 317 : 178, 318 : 178, 319 : 178, 320 : 178, 321 : 178, 322 : 178, 323 : 178, 324 : 178, 325 : 178, 326 : 178, 327 : 178, 328 : 178, 329 : 179, 330 : 179, 331 : 179, 332 : 179, 333 : 179, 334 : 179, 335 : 179, 336 : 179, 337 : 179, 338 : 179, 339 : 179, 340 : 179, 341 : 179, 342 : 179, 343 : 179, 344 : 179, 345 : 179, 346 : 179, 347 : 179, 348 : 179, 349 : 179, 350 : 180, 351 : 180, 352 : 180, 353 : 180, 354 : 180, 355 : 180, 356 : 180, 357 : 180, 358 : 180, 359 : 180, 360 : 180, 361 : 180, 362 : 180, 363 : 180, 364 : 180, 365 : 180, 366 : 180, 367 : 180, 368 : 180, 369 : 180, 370 : 180, 371 : 181, 372 : 181, 373 : 181, 374 : 181, 375 : 181, 376 : 181, 377 : 181, 378 : 181, 379 : 181, 380 : 181, 381 : 181, 382 : 181, 383 : 181, 384 : 181, 385 : 181, 386 : 181, 387 : 181, 388 : 181, 389 : 181, 390 : 181, 391 : 181, 392 : 181, 393 : 182, 394 : 182, 395 : 182, 396 : 182, 397 : 182, 398 : 182, 399 : 182, 400 : 182, 401 : 182, 402 : 182, 403 : 182, 404 : 182, 405 : 182, 406 : 182, 407 : 182, 408 : 182, 409 : 182, 410 : 182, 411 : 182, 412 : 182, 413 : 182, 414 : 183, 415 : 183, 416 : 183, 417 : 183, 418 : 183, 419 : 183, 420 : 183, 421 : 183, 422 : 183, 423 : 183, 424 : 183, 425 : 183, 426 : 183, 427 : 183, 428 : 183, 429 : 183, 430 : 183, 431 : 183, 432 : 183, 433 : 183, 434 : 183, 435 : 184, 436 : 184, 437 : 184, 438 : 184, 439 : 184, 440 : 184, 441 : 184, 442 : 184, 443 : 184, 444 : 184, 445 : 184, 446 : 184, 447 : 184, 448 : 184, 449 : 184, 450 : 184, 451 : 184, 452 : 184, 453 : 184, 454 : 184, 455 : 184, 456 : 185, 457 : 185, 458 : 185, 459 : 185, 460 : 185, 461 : 185, 462 : 185, 463 : 185, 464 : 185, 465 : 185, 466 : 185, 467 : 185, 468 : 185, 469 : 185, 470 : 185, 471 : 185, 472 : 185, 473 : 185, 474 : 185, 475 : 185, 476 : 185, 477 : 186, 478 : 186, 479 : 186, 480 : 186, 481 : 186, 482 : 186, 483 : 186, 484 : 186, 485 : 186, 486 : 186, 487 : 186, 488 : 186, 489 : 186, 490 : 186, 491 : 186, 492 : 186, 493 : 186, 494 : 186, 495 : 186, 496 : 186, 497 : 186, 498 : 186, 499 : 187, 500 : 187, 501 : 187, 502 : 187, 503 : 187, 504 : 187, 505 : 187, 506 : 187, 507 : 187, 508 : 187, 509 : 187, 510 : 187, 511 : 187, 512 : 187, 513 : 187, 514 : 187, 515 : 187, 516 : 187, 517 : 187, 518 : 187, 519 : 187, 520 : 188, 521 : 188, 522 : 188, 523 : 188, 524 : 188, 525 : 188, 526 : 188, 527 : 188, 528 : 188, 529 : 188, 530 : 188, 531 : 188, 532 : 188, 533 : 188, 534 : 188, 535 : 188, 536 : 188, 537 : 188, 538 : 188, 539 : 188, 540 : 188, 541 : 189, 542 : 189, 543 : 189, 544 : 189, 545 : 189, 546 : 189, 547 : 189, 548 : 189, 549 : 189, 550 : 189, 551 : 189, 552 : 189, 553 : 189, 554 : 189, 555 : 189, 556 : 189, 557 : 189, 558 : 189, 559 : 189, 560 : 189, 561 : 189, 562 : 190, 563 : 190, 564 : 190, 565 : 190, 566 : 190, 567 : 190, 568 : 190, 569 : 190, 570 : 190, 571 : 190, 572 : 190, 573 : 190, 574 : 190, 575 : 190, 576 : 190, 577 : 190, 578 : 190, 579 : 190, 580 : 190, 581 : 190, 582 : 190, 583 : 191, 584 : 191, 585 : 191, 586 : 191, 587 : 191, 588 : 191, 589 : 191, 590 : 191, 591 : 191, 592 : 191, 593 : 191, 594 : 191, 595 : 191, 596 : 191, 597 : 191, 598 : 191, 599 : 191, 600 : 191, 601 : 191, 602 : 191, 603 : 191, 604 : 192, 605 : 192, 606 : 192, 607 : 192, 608 : 192, 609 : 192, 610 : 192, 611 : 192, 612 : 192, 613 : 192, 614 : 192, 615 : 192, 616 : 192, 617 : 192, 618 : 192, 619 : 192, 620 : 192, 621 : 192, 622 : 192, 623 : 192, 624 : 192, 625 : 192, 626 : 193, 627 : 193, 628 : 193, 629 : 193, 630 : 193, 631 : 193, 632 : 193, 633 : 193, 634 : 193, 635 : 193, 636 : 193, 637 : 193, 638 : 193, 639 : 193, 640 : 193, 641 : 193, 642 : 193, 643 : 193, 644 : 193, 645 : 193, 646 : 193, 647 : 194, 648 : 194, 649 : 194, 650 : 194, 651 : 194, 652 : 194, 653 : 194, 654 : 194, 655 : 194, 656 : 194, 657 : 194, 658 : 194, 659 : 194, 660 : 194, 661 : 194, 662 : 194, 663 : 194, 664 : 194, 665 : 194, 666 : 194, 667 : 194, 668 : 195, 669 : 195, 670 : 195, 671 : 195, 672 : 195, 673 : 195, 674 : 195, 675 : 195, 676 : 195, 677 : 195, 678 : 195, 679 : 195, 680 : 195, 681 : 195, 682 : 195, 683 : 195, 684 : 195, 685 : 195, 686 : 195, 687 : 195, 688 : 195, 689 : 196, 690 : 196, 691 : 196, 692 : 196, 693 : 196, 694 : 196, 695 : 196, 696 : 196, 697 : 196, 698 : 196, 699 : 196, 700 : 196, 701 : 196, 702 : 196, 703 : 196, 704 : 196, 705 : 196, 706 : 196, 707 : 196, 708 : 196, 709 : 196, 710 : 197, 711 : 197, 712 : 197, 713 : 197, 714 : 197, 715 : 197, 716 : 197, 717 : 197, 718 : 197, 719 : 197, 720 : 197, 721 : 197, 722 : 197, 723 : 197, 724 : 197, 725 : 197, 726 : 197, 727 : 197, 728 : 197, 729 : 197, 730 : 197, 731 : 198, 732 : 198, 733 : 198, 734 : 198, 735 : 198, 736 : 198, 737 : 198, 738 : 198, 739 : 198, 740 : 198, 741 : 198, 742 : 198, 743 : 198, 744 : 198, 745 : 198, 746 : 198, 747 : 198, 748 : 198, 749 : 198, 750 : 198, 751 : 198, 752 : 198, 753 : 199, 754 : 199, 755 : 199, 756 : 199, 757 : 199, 758 : 199, 759 : 199, 760 : 199, 761 : 199, 762 : 199, 763 : 199, 764 : 199, 765 : 199, 766 : 199, 767 : 199, 768 : 199, 769 : 199, 770 : 199, 771 : 199, 772 : 199, 773 : 199, 774 : 200, 775 : 200, 776 : 200, 777 : 200, 778 : 200, 779 : 200, 780 : 200, 781 : 200, 782 : 200, 783 : 200, 784 : 200, 785 : 200, 786 : 200, 787 : 200, 788 : 200, 789 : 200, 790 : 200, 791 : 200, 792 : 200,
    },
    lightningDefenceTable: {
      82 : 13, 83 : 15, 84 : 16, 85 : 18, 86 : 19, 87 : 21, 88 : 22, 89 : 24, 90 : 25, 91 : 27, 92 : 28, 93 : 29, 94 : 31, 95 : 32, 96 : 34, 97 : 35, 98 : 37, 99 : 38, 100 : 40, 101 : 41, 102 : 43, 103 : 44, 104 : 46, 105 : 47, 106 : 49, 107 : 50, 108 : 52, 109 : 53, 110 : 54, 111 : 56, 112 : 57, 113 : 59, 114 : 60, 115 : 62, 116 : 63, 117 : 64, 118 : 66, 119 : 67, 120 : 69, 121 : 70, 122 : 71, 123 : 73, 124 : 74, 125 : 76, 126 : 77, 127 : 78, 128 : 80, 129 : 81, 130 : 83, 131 : 84, 132 : 85, 133 : 87, 134 : 88, 135 : 89, 136 : 91, 137 : 92, 138 : 93, 139 : 95, 140 : 96, 141 : 97, 142 : 99, 143 : 100, 144 : 101, 145 : 103, 146 : 104, 147 : 105, 148 : 106, 149 : 108, 150 : 109, 151 : 110, 152 : 111, 153 : 112, 154 : 114, 155 : 115, 156 : 116, 157 : 117, 158 : 118, 159 : 119, 160 : 120, 161 : 121, 162 : 121, 163 : 122, 164 : 122, 165 : 123, 166 : 124, 167 : 124, 168 : 125, 169 : 125, 170 : 126, 171 : 127, 172 : 127, 173 : 128, 174 : 128, 175 : 129, 176 : 129, 177 : 130, 178 : 131, 179 : 131, 180 : 132, 181 : 132, 182 : 133, 183 : 133, 184 : 134, 185 : 135, 186 : 135, 187 : 136, 188 : 136, 189 : 137, 190 : 137, 191 : 138, 192 : 138, 193 : 139, 194 : 140, 195 : 140, 196 : 141, 197 : 141, 198 : 142, 199 : 142, 200 : 143, 201 : 143, 202 : 144, 203 : 145, 204 : 145, 205 : 146, 206 : 146, 207 : 147, 208 : 147, 209 : 148, 210 : 148, 211 : 148, 212 : 148, 213 : 148, 214 : 148, 215 : 148, 216 : 148, 217 : 148, 218 : 148, 219 : 148, 220 : 153, 221 : 153, 222 : 153, 223 : 153, 224 : 155, 225 : 156, 226 : 156, 227 : 157, 228 : 157, 229 : 158, 230 : 158, 231 : 159, 232 : 159, 233 : 160, 234 : 160, 235 : 161, 236 : 161, 237 : 161, 238 : 162, 239 : 162, 240 : 163, 241 : 163, 242 : 164, 243 : 164, 244 : 164, 245 : 165, 246 : 165, 247 : 166, 248 : 166, 249 : 166, 250 : 167, 251 : 167, 252 : 168, 253 : 168, 254 : 168, 255 : 169, 256 : 169, 257 : 169, 258 : 170, 259 : 170, 260 : 170, 261 : 170, 262 : 170, 263 : 170, 264 : 170, 265 : 170, 266 : 170, 267 : 170, 268 : 170, 269 : 171, 270 : 171, 271 : 171, 272 : 171, 273 : 171, 274 : 171, 275 : 171, 276 : 171, 277 : 171, 278 : 171, 279 : 171, 280 : 171, 281 : 171, 282 : 171, 283 : 171, 284 : 171, 285 : 171, 286 : 171, 287 : 172, 288 : 172, 289 : 172, 290 : 172, 291 : 172, 292 : 172, 293 : 172, 294 : 172, 295 : 172, 296 : 172, 297 : 172, 298 : 172, 299 : 172, 300 : 172, 301 : 172, 302 : 172, 303 : 172, 304 : 172, 305 : 173, 306 : 173, 307 : 173, 308 : 173, 309 : 173, 310 : 173, 311 : 173, 312 : 173, 313 : 173, 314 : 173, 315 : 173, 316 : 173, 317 : 173, 318 : 173, 319 : 173, 320 : 173, 321 : 173, 322 : 173, 323 : 174, 324 : 174, 325 : 174, 326 : 174, 327 : 174, 328 : 174, 329 : 174, 330 : 174, 331 : 174, 332 : 174, 333 : 174, 334 : 174, 335 : 174, 336 : 174, 337 : 174, 338 : 174, 339 : 174, 340 : 174, 341 : 175, 342 : 175, 343 : 175, 344 : 175, 345 : 175, 346 : 175, 347 : 175, 348 : 175, 349 : 175, 350 : 175, 351 : 175, 352 : 175, 353 : 175, 354 : 175, 355 : 175, 356 : 175, 357 : 175, 358 : 175, 359 : 176, 360 : 176, 361 : 176, 362 : 176, 363 : 176, 364 : 176, 365 : 176, 366 : 176, 367 : 176, 368 : 176, 369 : 176, 370 : 176, 371 : 176, 372 : 176, 373 : 176, 374 : 176, 375 : 176, 376 : 176, 377 : 177, 378 : 177, 379 : 177, 380 : 177, 381 : 177, 382 : 177, 383 : 177, 384 : 177, 385 : 177, 386 : 177, 387 : 177, 388 : 177, 389 : 177, 390 : 177, 391 : 177, 392 : 177, 393 : 177, 394 : 177, 395 : 178, 396 : 178, 397 : 178, 398 : 178, 399 : 178, 400 : 178, 401 : 178, 402 : 178, 403 : 178, 404 : 178, 405 : 178, 406 : 178, 407 : 178, 408 : 178, 409 : 178, 410 : 178, 411 : 178, 412 : 178, 413 : 179, 414 : 179, 415 : 179, 416 : 179, 417 : 179, 418 : 179, 419 : 179, 420 : 179, 421 : 179, 422 : 179, 423 : 179, 424 : 179, 425 : 179, 426 : 179, 427 : 179, 428 : 179, 429 : 179, 430 : 179, 431 : 180, 432 : 180, 433 : 180, 434 : 180, 435 : 180, 436 : 180, 437 : 180, 438 : 180, 439 : 180, 440 : 180, 441 : 180, 442 : 180, 443 : 180, 444 : 180, 445 : 180, 446 : 180, 447 : 180, 448 : 180, 449 : 181, 450 : 181, 451 : 181, 452 : 181, 453 : 181, 454 : 181, 455 : 181, 456 : 181, 457 : 181, 458 : 181, 459 : 181, 460 : 181, 461 : 181, 462 : 181, 463 : 181, 464 : 181, 465 : 181, 466 : 181, 467 : 182, 468 : 182, 469 : 182, 470 : 182, 471 : 182, 472 : 182, 473 : 182, 474 : 182, 475 : 182, 476 : 182, 477 : 182, 478 : 182, 479 : 182, 480 : 182, 481 : 182, 482 : 182, 483 : 182, 484 : 182, 485 : 183, 486 : 183, 487 : 183, 488 : 183, 489 : 183, 490 : 183, 491 : 183, 492 : 183, 493 : 183, 494 : 183, 495 : 183, 496 : 183, 497 : 183, 498 : 183, 499 : 183, 500 : 183, 501 : 183, 502 : 183, 503 : 184, 504 : 184, 505 : 184, 506 : 184, 507 : 184, 508 : 184, 509 : 184, 510 : 184, 511 : 184, 512 : 184, 513 : 184, 514 : 184, 515 : 184, 516 : 184, 517 : 184, 518 : 184, 519 : 184, 520 : 184, 521 : 185, 522 : 185, 523 : 185, 524 : 185, 525 : 185, 526 : 185, 527 : 185, 528 : 185, 529 : 185, 530 : 185, 531 : 185, 532 : 185, 533 : 185, 534 : 185, 535 : 185, 536 : 185, 537 : 185, 538 : 185, 539 : 186, 540 : 186, 541 : 186, 542 : 186, 543 : 186, 544 : 186, 545 : 186, 546 : 186, 547 : 186, 548 : 186, 549 : 186, 550 : 186, 551 : 186, 552 : 186, 553 : 186, 554 : 186, 555 : 186, 556 : 186, 557 : 187, 558 : 187, 559 : 187, 560 : 187, 561 : 187, 562 : 187, 563 : 187, 564 : 187, 565 : 187, 566 : 187, 567 : 187, 568 : 187, 569 : 187, 570 : 187, 571 : 187, 572 : 187, 573 : 187, 574 : 187, 575 : 188, 576 : 188, 577 : 188, 578 : 188, 579 : 188, 580 : 188, 581 : 188, 582 : 188, 583 : 188, 584 : 188, 585 : 188, 586 : 188, 587 : 188, 588 : 188, 589 : 188, 590 : 188, 591 : 188, 592 : 188, 593 : 189, 594 : 189, 595 : 189, 596 : 189, 597 : 189, 598 : 189, 599 : 189, 600 : 189, 601 : 189, 602 : 189, 603 : 189, 604 : 189, 605 : 189, 606 : 189, 607 : 189, 608 : 189, 609 : 189, 610 : 189, 611 : 190, 612 : 190, 613 : 190, 614 : 190, 615 : 190, 616 : 190, 617 : 190, 618 : 190, 619 : 190, 620 : 190, 621 : 190, 622 : 190, 623 : 190, 624 : 190, 625 : 190, 626 : 190, 627 : 190, 628 : 190, 629 : 191, 630 : 191, 631 : 191, 632 : 191, 633 : 191, 634 : 191, 635 : 191, 636 : 191, 637 : 191, 638 : 191, 639 : 191, 640 : 191, 641 : 191, 642 : 191, 643 : 191, 644 : 191, 645 : 191, 646 : 191, 647 : 192, 648 : 192, 649 : 192, 650 : 192, 651 : 192, 652 : 192, 653 : 192, 654 : 192, 655 : 192, 656 : 192, 657 : 192, 658 : 192, 659 : 192, 660 : 192, 661 : 192, 662 : 192, 663 : 192, 664 : 192, 665 : 193, 666 : 193, 667 : 193, 668 : 193, 669 : 193, 670 : 193, 671 : 193, 672 : 193, 673 : 193, 674 : 193, 675 : 193, 676 : 193, 677 : 193, 678 : 193, 679 : 193, 680 : 193, 681 : 193, 682 : 193, 683 : 194, 684 : 194, 685 : 194, 686 : 194, 687 : 194, 688 : 194, 689 : 194, 690 : 194, 691 : 194, 692 : 194, 693 : 194, 694 : 194, 695 : 194, 696 : 194, 697 : 194, 698 : 194, 699 : 194, 700 : 194, 701 : 195, 702 : 195, 703 : 195, 704 : 195, 705 : 195, 706 : 195, 707 : 195, 708 : 195, 709 : 195, 710 : 195, 711 : 195, 712 : 195, 713 : 195, 714 : 195, 715 : 195, 716 : 195, 717 : 195, 718 : 195, 719 : 196, 720 : 196, 721 : 196, 722 : 196, 723 : 196, 724 : 196, 725 : 196, 726 : 196, 727 : 196, 728 : 196, 729 : 196, 730 : 196, 731 : 196, 732 : 196, 733 : 196, 734 : 196, 735 : 196, 736 : 196, 737 : 197, 738 : 197, 739 : 197, 740 : 197, 741 : 197, 742 : 197, 743 : 197, 744 : 197, 745 : 197, 746 : 197, 747 : 197, 748 : 197, 749 : 197, 750 : 197, 751 : 197, 752 : 197, 753 : 197, 754 : 197, 755 : 198, 756 : 198, 757 : 198, 758 : 198, 759 : 198, 760 : 198, 761 : 198, 762 : 198, 763 : 198, 764 : 198, 765 : 198, 766 : 198, 767 : 198, 768 : 198, 769 : 198, 770 : 198, 771 : 198, 772 : 198, 773 : 199, 774 : 199, 775 : 199, 776 : 199, 777 : 199, 778 : 199, 779 : 199, 780 : 199, 781 : 199, 782 : 199, 783 : 199, 784 : 199, 785 : 199, 786 : 199, 787 : 199, 788 : 199, 789 : 199, 790 : 199, 791 : 200, 792 : 200, 
    },
  }),
  computed: {},
  watch: {
    //Watch for when user updates the stats on their build and update the statsum and defences accordingly
    characterStats: {
      handler(newVal) {
        // if (newVal.resistance !== oldVal.resistance) {
        //   this.characterResistanceStat = newVal.resistance
        // }
        this.characterResistanceStat = newVal.resistance
        this.getStatSum(newVal)
        
        this.calculateDefence(this.statSum, this.characterResistanceStat)
        this.calculateElementalDefence(this.statSum, this.characterResistanceStat, "fire")
        this.calculateElementalDefence(this.statSum, newVal.faith, "magic")
        this.calculateElementalDefence(this.statSum, null, "lightning")
      },
      deep: true
    }
  },
  methods: {
    getStatSum(characterStats) {
      let sum = 0
      //Get the sum of all stats
      Object.keys(characterStats).forEach(key => {
        if (Number.isInteger(characterStats[key]) && key !== "level") {
          sum += characterStats[key]
        }
      })
      
      this.statSum = sum
    },
    calculateDefence(statSum, resistance) {
      let lookupIndex = statSum + resistance - 8
      //console.log(lookupIndex)
      // if lookup index determined by stat sum and the players resistance stat are below the scaling softcap 
      // do not add diminishing returns with harsher lookup
      if (lookupIndex < 262) {
        //console.log(lookupIndex)
        this.physicalDefence.physical = this.physicalDefenceTable[lookupIndex]
        this.physicalDefence.slash = this.physicalDefenceTable[lookupIndex]
        this.physicalDefence.strike = this.physicalDefenceTable[lookupIndex]
        this.physicalDefence.thrust = this.physicalDefenceTable[lookupIndex]
      } else {
        lookupIndex = statSum + resistance - 99
        //console.log(lookupIndex)
        this.physicalDefence.physical = this.physicalDefence99Table[lookupIndex]
        this.physicalDefence.slash = this.physicalDefence99Table[lookupIndex]
        this.physicalDefence.strike = this.physicalDefence99Table[lookupIndex]
        this.physicalDefence.thrust = this.physicalDefence99Table[lookupIndex]
      }
    },
    calculateElementalDefence(statSum, scalingStat, elementType) {
      let lookupIndex
      //If calculating lightning defence - take sum of stats and use value against table
      if (elementType == "lightning") {
         this.elementalDefence.lightning = this.lightningDefenceTable[statSum]
         return
      }
      //if sum of stats and adjusted scaling stat are higher than softcap for defence - defence should return diminishing returns against harsher lookup
      if (statSum + Math.floor((scalingStat - 8) * 1.59) > 325) {
        lookupIndex = statSum + Math.floor((scalingStat - 99) * 1.59)
        this.elementalDefence[elementType] = this.magFireDefence99Table[lookupIndex]
      } else {
        lookupIndex = statSum +  Math.floor((scalingStat - 8) * 1.59)
        this.elementalDefence[elementType] = this.magFireDefenceTable[lookupIndex]
      }
    },
  },
  created() {
    console.log(this.characterStats)
    this.getStatSum(this.characterStats)
    this.characterResistanceStat = this.characterStats.resistance
    this.characterFaithStat = this.characterStats.faith
    
    this.calculateDefence(this.statSum, this.characterResistanceStat)
    this.calculateElementalDefence(this.statSum, this.characterResistanceStat, "fire")
    this.calculateElementalDefence(this.statSum, this.characterStats.faith, "magic")
    this.calculateElementalDefence(this.statSum, null, "lightning")
  }
}
</script>

<style lang="scss">
.defence-stats {
  //padding-top: 2em;
  table {
    tbody {
      tr.tr-head {
        text-align: left;
      }
      tr.tr-subhead {
        padding-left: 2em;
      }
    }
  }
}
</style>