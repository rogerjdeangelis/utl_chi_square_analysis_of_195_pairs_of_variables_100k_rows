# utl_chi_square_analysis_of_195_pairs_of_variables_100k_rows
Chi square analysis of 195 pairs of variables and 100k rows.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Chi square analysis of 195 pairs of variables and 100k rows

    github
    https://tinyurl.com/ybnmc9ux
    https://github.com/rogerjdeangelis/utl_chi_square_analysis_of_195_pairs_of_variables_100k_rows

    I suggest you use data_null_s by processing but I did 195 chi square analyses
    in 20 seconds.

    INPUT
    =====

    WORK.HAVE total obs=100,000

      Obs f1 f2 f3 f4 f5  .. f194   b1 b2 b3 b4 b5  .. b195

        1 24 38 25  3 44      19     8  9  8 10 14      12
        2 33 31 91 71 56      72    79 30 57 74 89      24
        3 82 99 17 23 85      65    60 68 42  4 54       8
        4 41 25 15 18 97      49     3 38 43 81 72      42
        5 11 70 62 90 69      89    25  2  8 54 64      97
        6 67 38 97 47 10      65    98 33 49  8 56       2
        7 75 39 87 12  8      21    21 21 93 63 99      73
        8 61 98 73 29 37      90    34 50 46 61 24       7
        9 49 16 57 85 53      34    26 99 56 73 88      87
     ...
     9999 24 38 25  3 44      19     8  9  8 10 14      12
    10000 75 39 87 12  8      21    21 21 93 63 99      73

    OUTPUT
    ======

     WORK.CHIS total obs=195

         Table            Statistic      DF       Value       Prob

     Table f1 * b1        Chi-Square    9801    10012.62    0.06610
     Table f2 * b2        Chi-Square    9801     9864.85    0.32282
     Table f3 * b3        Chi-Square    9801     9600.25    0.92493

     Table f195 * b195    Chi-Square    9801     8976.25    0.87653

    PROCESS
    =======

      %utlnopts; * not needed but turns off the log - saves time;

      sasfile have load; * I like to put the data in memory - not needed;

      %array(fb,values=1-195);

      ods exclude all;
      ods output chisq=chis(where=(statistic='Chi-Square'));

      proc freq data=have;
       table

         %do_over(fb,phrase=f? * b?)

         / chisq missing;
      run;quit;

      ods select all;

      sasfile have close;

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    if the numder of observartions is not too large sat
    less that 100,000,000 then then the following mab be workable.

    store your dataset in memory, I have 64gb ram on my $600 workstation;

    data have;

      array fs[195] f1-f195;
      array bs[195] b1-b195;

      do rec=1 to 100000;
         do i=1 to 195;
           fs[i]=int(100*uniform(1234));
           bs[i]=int(100*uniform(4567));
         end;
         output;
      end;
      drop i;
    run;quit;

