# utl-sort-a-sequence-of-numbers-or-words-using-sas-macro
utl sort a macro string of words sortc and dosubl (without loops) 
    %let pgm=utl-sort-a-sequence-of-numbers-or-words-using-sas-macro;

    %stop_submission;

    utl sort a macro string of words sortc and dosubl (without loops)

      1 macro utl_sortn
      2 macro utl_sortc

     related repo
     https://stackoverflow.com/users/4965549/tom

     github
     https://tinyurl.com/bdcv76ed
     https://github.com/rogerjdeangelis/utl-sort-a-sequence-of-numbers-or-words-using-sas-macro

     Interesting points?

       1  Evaluate a macro variable withib single quotes
          %let buff=%sysfunc(dequote("'&buff'"));

       2  Evaluate macro variables inside dosubl
          I could not get nrstr to work


    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                          |                                                          |                                  */
    /*         INPUT            |           PROCESS                                        | OUTPUT                           */
    /*                          |                                                          |                                  */
    /*  SORT NUMBERS            |                                                          |                                  */
    /*  ============            |                                                          |                                  */
    /*                          |                                                          |                                  */
    /*  Macro string = 4 3 2 1  | %macro utl_sortn() / parmbuff ;                          | Sorted numbers                   */
    /*                          |                                                          |                                  */
    /*                          |   %local n rc list buff;                                 | %put xx %utl_sortn(4 3 2 1) xx;  */
    /*                          |                                                          |                                  */
    /*                          |   %let n=%sysfunc(countw(&syspbuff,( , )));              | xx   1 2 3 4 xx                  */
    /*                          |                                                          |                                  */
    /*                          |   %dosubl(%sysfunc(dequote("                             |                                  */
    /*                          |      data _null_;                                        |                                  */
    /*                          |        array x [&n] _temporary_ &syspbuff;               |                                  */
    /*                          |        call sortn(of x[*]);                              |                                  */
    /*                          |        call symputx('_sessref_',catx(' ',of x[*]));      |                                  */
    /*                          |      run;                                                |                                  */
    /*                          |      ")))                                                |                                  */
    /*                          |                                                          |                                  */
    /*                          |   &_sessref_                                             |                                  */
    /*                          |                                                          |                                  */
    /*                          | %mend utl_sortn;                                         |                                  */
    /*                          |                                                          |                                  */
    /*                          | %put xx %utl_sortn(4 3 2 1) xx;                          |                                  */
    /*                          |                                                          |                                  */
    /*                          |                                                          |                                  */
    /*  SORT WORDS              |                                                          |                                  */
    /*  ==========              |                                                          |                                  */
    /*                          |                                                          |                                  */
    /*  Macro string = d c b a  | %macro utl_sortc(buff) ;                                 | Sorted numbers                   */
    /*                          |                                                          |                                  */
    /*                          | %local n rc buff ;                                       | %put xx %utl_sortn(d c b a) xx;  */
    /*                          |                                                          |                                  */
    /*                          | %let n=%sysfunc(countw(&buff));                          | xx   a b c d xx                  */
    /*                          |                                                          |                                  */
    /*                          | %let buff=%sysfunc(dequote("'&buff'"));                  |                                  */
    /*                          | %let buff=%qsysfunc(tranwrd(&buff,%str( ),%str(' ')));   |                                  */
    /*                          |                                                          |                                  */
    /*                          | %dosubl(%sysfunc(dequote("                               |                                  */
    /*                          |   data _null_;                                           |                                  */
    /*                          |     array x [&n] $32 _temporary_ (&buff);                |                                  */
    /*                          |     call sortc(of x[*]);                                 |                                  */
    /*                          |     call symputx('_sessref_',catx(' ',of x[*]));         |                                  */
    /*                          |   run;quit;                                              |                                  */
    /*                          |   ")))                                                   |                                  */
    /*                          |                                                          |                                  */
    /*                          |   &_sessref_                                             |                                  */
    /*                          |                                                          |                                  */
    /*                          | %mend;                                                   |                                  */
    /*                          |                                                          |                                  */
    /*                          | %put xx %utl_sortc(d c b a) xx;                          |                                  */
    /*                          |                                                          |                                  */
    /**************************************************************************************************************************/

    /*                                          _   _                  _
    / |  _ __ ___   __ _  ___ _ __ ___    _   _| |_| |  ___  ___  _ __| |_ _ __
    | | | `_ ` _ \ / _` |/ __| `__/ _ \  | | | | __| | / __|/ _ \| `__| __| `_ \
    | | | | | | | | (_| | (__| | | (_) | | |_| | |_| | \__ \ (_) | |  | |_| | | |
    |_| |_| |_| |_|\__,_|\___|_|  \___/   \__,_|\__|_|_|___/\___/|_|   \__|_| |_|
     _                   _                            |___|
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Macro string = 4 3 2 1                                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    /*----                                                                   ----*/
    /*---- probably not needed (clear environment                            ----*/
    /*----                                                                   ----*/
    proc datasets lib=work nolist nodetails mt=data mt=cat;
          delete sasmac1 sasmac2 sasmac3 sasmac4; * probably not needed;
    run;quit;

    %let _sessref_=null;
    %put &=_sessref_;


    %macro utl_sortn() / parmbuff ;

      %local n rc buff;

      %let n=%sysfunc(countw(&syspbuff,( , )));

      %dosubl(%sysfunc(dequote("
         data _null_;
           array x [&n] _temporary_ &syspbuff;
           call sortn(of x[*]);
           call symputx('_sessref_',catx(' ',of x[*]));
         run;
         ")))

      &_sessref_

    %mend utl_sortn;

    %put xx %utl_sortn(4 3 2 1) xx;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Sorted numbers                                                                                                         */
    /*                                                                                                                        */
    /* %put xx %utl_sortn(4 3 2 1) xx;                                                                                        */
    /*                                                                                                                        */
    /* xx   1 2 3 4 xx                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                                                    _
    |___ \   _ __ ___   __ _  ___ _ __ ___    ___  ___  _ __| |_ ___
      __) | | `_ ` _ \ / _` |/ __| `__/ _ \  / __|/ _ \| `__| __/ __|
     / __/  | | | | | | (_| | (__| | | (_) | \__ \ (_) | |  | || (__
    |_____| |_| |_| |_|\__,_|\___|_|  \___/__|___/\___/|_|   \__\___|
     _                   _                |___|
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SORT WORDS                                                                                                            */
    /*  ==========                                                                                                            */
    /*                                                                                                                        */
    /*  Macro string = d c b a                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    /*----                                                                   ----*/
    /*---- probably not needed (clear environment                            ----*/
    /*----                                                                   ----*/
    proc datasets lib=work nolist nodetails mt=data mt=cat;
          delete sasmac1 sasmac2 sasmac3 sasmac4; * probably not needed;
    run;quit;

    %let _sessref_=null;
    %put &=_sessref_;



    %macro utl_sortc(buff) ;

    %local n rc buff ;

    %let n=%sysfunc(countw(&buff));

    %let buff=%sysfunc(dequote("'&buff'"));
    %let buff=%qsysfunc(tranwrd(&buff,%str( ),%str(' ')));

    %dosubl(%sysfunc(dequote("
      data _null_;
        array x [&n] $32 _temporary_ (&buff);
        call sortc(of x[*]);
        call symputx('_sessref_',catx(' ',of x[*]));
      run;quit;
      ")))

      &_sessref_

    %mend;

    %put xx %utl_sortc(d c b a) xx;


    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Sorted numbers                                                                                                         */
    /*                                                                                                                        */
    /* %put xx %utl_sortn(d c b a) xx;                                                                                        */
    /*                                                                                                                        */
    /* xx   a b c d xx                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
