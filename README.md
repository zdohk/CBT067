~~~~~~~~~~~~~~~~

//***FILE 067 IS FROM COCA COLA IN ATLANTA AND CONTAINS TWO EXITS   *   FILE 067
//*           THAT ARE USED TO CONTROL VIO ALLOCATION, SIZE,        *   FILE 067
//*           FORCE TSO TEMPORARY DATA SETS TO DEDICATED TSO        *   FILE 067
//*           "PUBLIC" VOLUMES AND A FEW OTHER MISCELLANEOUS        *   FILE 067
//*           FUNCTIONS.  THIS FILE IS IN IEBUDPTE SYSIN FORMAT     *   FILE 067
//*           AND CONTAINS THE FOLLOWING :                          *   FILE 067
//*                                                                 *   FILE 067
//*            IEFDB401:                                            *   FILE 067
//*                                                                 *   FILE 067
//*              SVC99 EXIT TO ALLOCATE TSO TEMPORARY DATASETS TO   *   FILE 067
//*              A TSO ONLY SCRATCH PACK AND CONTROL THE SIZE OF    *   FILE 067
//*              VIO DATA SETS FROM TSO.  THIS EXIT CHANGES THE     *   FILE 067
//*              UNIT NAME FOR ALL DYNAMIC ALLOCATIONS TO SUPPORT   *   FILE 067
//*              THE FOLLOWING FUNCTIONS:                           *   FILE 067
//*                                                                 *   FILE 067
//*                 1) CONTROL VIO ALLOCATION SIZE.  THIS REQUIRES  *   FILE 067
//*                     THE USER TO SPECIFY UNIT(VIOALLOC).         *   FILE 067
//*                     UNIT=VIOALLOC IS NOT VALID IN THE SYSGEN    *   FILE 067
//*                     PARAMETERS.  IF THE SPACE= SPECIFIES A      *   FILE 067
//*                     VALID AMOUNT OF DISK SPACE, THE UNIT= IS    *   FILE 067
//*                     CHANGED TO UNIT=VIODA WHICH IS A 3340.  IF  *   FILE 067
//*                     UNIT=VIODA IS CODED IN THE JCL OR THE       *   FILE 067
//*                     SPACE= IS TOO LARGE, THE UNIT= IS CHANGED   *   FILE 067
//*                     TO UNIT=SYSDA.                              *   FILE 067
//*                                                                 *   FILE 067
//*                 2) FORCE TSO TEMPORARY DATASETS TO A DEDICATED  *   FILE 067
//*                     "PUBLIC" VOLUME.  UNIT(VIOALLOC) IS         *   FILE 067
//*                     SPECIFIED TO INVOKE THIS SERVICE.  IF THE   *   FILE 067
//*                     SPACE= IS MET IN 1) ABOVE, THE DATASET GOES *   FILE 067
//*                     TO VIO; OTHERWISE A CHECK IS MADE TO VERIFY *   FILE 067
//*                     THAT THE DYNAMIC ALLOCATION IS MADE BY A    *   FILE 067
//*                     TSO USER.  IF IT IS A TSO USER, UNIT=TSODA  *   FILE 067
//*                     IS USED TO FORCE TSO DATASETS TO DEDICATED  *   FILE 067
//*                     TSO "PUBLIC" VOLUMES.  ANY ATTEMPT TO CODE  *   FILE 067
//*                     UNIT(TSODA) IS REPLACED BY UNIT(SYSDA).     *   FILE 067
//*                                                                 *   FILE 067
//*                 3) VERIFY THAT ALL IMS ALLOCATION OF AN         *   FILE 067
//*                     INTERNAL READER COMES FROM PROGRAM          *   FILE 067
//*                     O9061S75.  THIS IS TO ENSURE THAT ACF2 HAS  *   FILE 067
//*                     THE CORRECT SYSTEM ID FOR JOBS SUBMITTED BY *   FILE 067
//*                     IMS TRANSACTIONS.  AN ATTEMPT TO VIOLATE    *   FILE 067
//*                     ACF2 REQUIREMENTS GETS THE USER A S0C3.     *   FILE 067
//*                                                                 *   FILE 067
//*                 4) UNIT=DISK IS SUBSTITUTED FOR ALL UNIT=XXXX   *   FILE 067
//*                     WHERE XXXX IS EXACTLY FOUR CHARACTERS LONG. *   FILE 067
//*                                                                 *   FILE 067
//*            IEFUJV:                                              *   FILE 067
//*                                                                 *   FILE 067
//*              SMF EXIT TO CHANGE JCL TO MEET COMPANY STANDARDS.  *   FILE 067
//*              IT SUPPORTS THE MSVGP= PARAMETER FOR A NON-3850    *   FILE 067
//*              ENVIRONMENT, CONTROLS VIO SPACE ALLOCATION AND     *   FILE 067
//*              SEVERAL OTHER MISCELLANEOUS FUNCTIONS.  SUPPORTS   *   FILE 067
//*              THE FOLLOWING FUNCTIONS:                           *   FILE 067
//*                                                                 *   FILE 067
//*               I. JOB CARD -- NO ACTION                          *   FILE 067
//*                                                                 *   FILE 067
//*              II. EXEC CARD                                      *   FILE 067
//*                                                                 *   FILE 067
//*                 1) WRITE AN SMF TYPE 131 RECORD IF A PROC IS    *   FILE 067
//*                     EXECUTED.  THIS IS TO ALLOW DETERMINATION   *   FILE 067
//*                     WHICH PROCS ARE USED AND WHICH ARE NOT      *   FILE 067
//*                                                                 *   FILE 067
//*             III. DD CARD                                        *   FILE 067
//*                                                                 *   FILE 067
//*                 1) CONTROL VIO ALLOCATION SIZE.  THIS REQUIRES  *   FILE 067
//*                     THE USER TO SPECIFY UNIT=VIOALLOC.          *   FILE 067
//*                     UNIT=VIOALLOC IS NOT VALID IN THE SYSGEN    *   FILE 067
//*                     PARAMETERS.  IF THE SPACE= SPECIFIES A      *   FILE 067
//*                     VALID AMOUNT OF DISK SPACE, THE UNIT= IS    *   FILE 067
//*                     CHANGED TO UNIT=VIODA WHICH IS A 3340.  IF  *   FILE 067
//*                     UNIT=VIODA IS CODED IN THE JCL OR THE       *   FILE 067
//*                     SPACE= IS TOO LARGE, THE UNIT= IS CHANGED   *   FILE 067
//*                     TO UNIT=SYSDA.  THIS JOB HAS THE NAME OF    *   FILE 067
//*                     TWO BATCH JOBS THAT ARE ALLOWED TO USE VIO, *   FILE 067
//*                     OTHERWISE VIO IS RESTRICTED TO TSO USERS    *   FILE 067
//*                     ONLY.  BOTH UNIT= AND SPACE= MUST BE ON THE *   FILE 067
//*                     SAME CARD FOR THIS TO WORK.  UNIT= MUST     *   FILE 067
//*                     ALSO BE THE LAST PARAMETER ON THE LAST CARD *   FILE 067
//*                     OF A DD CARD CONCATENATION.                 *   FILE 067
//*                                                                 *   FILE 067
//*                 2) FORCE TSO TEMPORARY DATASETS TO A DEDICATED  *   FILE 067
//*                     "PUBLIC" VOLUME.  UNIT=VIOALLOC IS          *   FILE 067
//*                     SPECIFIED TO INVOKE THIS SERVICE.  IF THE   *   FILE 067
//*                     SPACE= IS MET IN 1) ABOVE, THE DATASET GOES *   FILE 067
//*                     TO VIO; OTHERWISE A CHECK IS MADE TO VERIFY *   FILE 067
//*                     THAT THE DYNAMIC ALLOCATION IS MADE BY A    *   FILE 067
//*                     TSO USER.  IF IT IS A TSO USER, UNIT=TSODA  *   FILE 067
//*                     IS USED TO FORCE TSO DATASETS TO DEDICATED  *   FILE 067
//*                     TSO "PUBLIC" VOLUMES.  ANY ATTEMPT TO CODE  *   FILE 067
//*                     UNIT(TSODA) IS REPLACED BY UNIT(SYSDA).     *   FILE 067
//*                     BOTH UNIT= AND SPACE= MUST BE ON THE SAME   *   FILE 067
//*                     CARD FOR THIS TO WORK.                      *   FILE 067
//*                                                                 *   FILE 067
//*                 3) MSVGP=GDGDAN IS OUR INSTALLATION             *   FILE 067
//*                     SPECIFICATION FOR DISK GDG DATASETS         *   FILE 067
//*                     (CURRENTLY 2 3380-BE4 UNITS WORTH).  THE    *   FILE 067
//*                     CODE TO IMPLEMENT THIS IS IN THIS EXIT.     *   FILE 067
//*                     MSVGP= MUST BE THE ONLY USEFUL INFORMATION  *   FILE 067
//*                     ON THE LAST CARD OF A DD CARD CONTINUATION  *   FILE 067
//*                     FOR THIS TO WORK BECAUSE THE ENTIRE CARD IS *   FILE 067
//*                     REPLACED.                                   *   FILE 067
//*                                                                 *   FILE 067
//*                 4) THE ARCHAIC FORM OF THE INTERNAL READER IS   *   FILE 067
//*                     CHANGED TO THE CURRENTLY SUPPORTED VERSION. *   FILE 067
//*                                                                 *   FILE 067
~~~~~~~~~~~~~~~~

