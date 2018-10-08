# utl-computing-counts-using-sql-arrays
Computing counts using sql arrays.
    Computing counts usin sql arrays

    github
    https://github.com/rogerjdeangelis/utl-computing-counts-using-sql-arrays

    SAS Forum
    https://communities.sas.com/t5/SAS-Programming/Arrays/m-p/502465


    INPUT
    =====

    WORK.HAVE total obs=51

    Obs    VARS      | RULES
                     |
      1    D801      |  Count D801 there are 9
      2    D839      |
      3    D830      |
      4    D806      |
      5    D803      |
    ...              |
     50    D830      |
     51    D806      |

    EXAMPLE OUTPUT
    ==============

    WORK .WANT total obs=1

      COUNT D801 D803 D804 D806 D808 D809 D829 D830 D838 D839 D849 D899

      COUNT    9    4    2    3    1    1    1    2    3   22    1    2


    PROCESS
    =======

    proc sql;
      select distinct vars into :vars separated by " " from have
    ;quit;

    %array(vrs,values=&vars)

    proc sql;
      create table want as
      select 'count' as count
      ,%do_over(vrs,phrase=sum(vars="?") as ?,between=comma)
      from have
    ;quit;

    /* Generated code

    , sum(vars="D803") as D803
    , sum(vars="D804") as D804
    , sum(vars="D806") as D806
    , sum(vars="D808") as D808
    , sum(vars="D809") as D809
    , sum(vars="D829") as D829
    , sum(vars="D830") as D830
    , sum(vars="D838") as D838
    , sum(vars="D839") as D839
    , sum(vars="D849") as D849
    , sum(vars="D899") as D899

    */

    OUTPUT
    ======

    WORK .WANT total obs=1

      COUNT D801 D803 D804 D806 D808 D809 D829 D830 D838 D839 D849 D899

      COUNT    9    4    2    3    1    1    1    2    3   22    1    2


    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data have;
     input vars$ @@;
     vars=compress(vars,'.');
     if vars ne '9999' then output;
    cards4;
    D80.1 9999 9999
    D83.9 D83.0 D80.6
    D80.3 9999 9999
    D83.9 9999 9999
    D82.9 9999 9999
    D83.9 9999 9999
    D83.9 9999 9999
    D83.9 9999 9999
    D83.0 9999 9999
    D80.6 9999 9999
    D83.9 9999 D80.4
    D83.8 D89.9 9999
    D80.1 9999 9999
    D83.9 9999 9999
    D83.9 9999 9999
    D83.9 9999 9999
    D80.1 9999 9999
    D80.1 D83.9 D80.4
    D83.9 9999 9999
    D83.9 9999 9999
    D80.1 D83.9 D83.9
    D84.9 D80.3 9999
    D80.9 9999 9999
    D83.9 9999 9999
    D83.9 D83.8 9999
    D83.8 9999 9999
    D80.1 D80.8 D89.9
    D80.6 9999 9999
    D80.1 9999 9999
    D80.1 9999 9999
    D83.9 9999 9999
    D80.1 9999 9999
    D83.9 9999 9999
    D83.9 9999 9999
    D83.9 D80.3 9999
    D83.9 9999 D80.3
    D83.9 9999 9999
    ;;;;
    run;quit;

