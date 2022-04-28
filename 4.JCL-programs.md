1. Write a JCL program to allocate PS file with Name - Myporj.EMP.Details in Volume ZAPRD4 with storage of 5 tracks and 2 
    tracks of extended having format as fixed block type and logical record length of 80.
      ```
      //HRIT80A JOB 123,",", CLASS= A, MSGCLASS=A,MSGLEVEL=(0,1),NOTIFY=&SYSUID
      //STEP01 EXEC PGM=IEFBR14
      //DD0101 DD DSN=HRIT80A.MYPROJ.EMP.DETAILS,
      //          DISP=(NEW,CATLG,DELETE),
      //          SPACE=(TRK,(5,2),RLSE),
      //          VOL=SER=ZAPRD4,
      //          DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800),
      //          UNIT=SYSDA
      //SYSOUT DD SYSOUT=*
      ```
  
2. Write a JCL program to allocate PDS file with Name - Myporj.Monthly.Reports in Volume ZAPRD4 with 5 tracks of primary memory, 2 
    tracks of extended memory and 5 directory blocks having fixed block as record format, logical record length of 80 and block size 800.
      ```
      //HRIT80A JOB 123,",", CLASS= A, MSGCLASS=A,MSGLEVEL=(0,1),NOTIFY=&SYSUID
      //STEP01 EXEC PGM=IEFBR14
      //DD0101 DD DSN=HRIT80A.MYPROJ.MONTHLY.REPORTS,
      //          DISP=(NEW,CATLG,DELETE),
      //          SPACE=(TRK,(5,2,5),RLSE),
      //          VOL=SER=ZAPRD4,
      //          DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800),
      //          UNIT=SYSDA
      //SYSOUT DD SYSOUT=*
      ```
      
3. Write a 2 step JCL program to allocate PS file with Name - Myporj.Customer.Details and PDS file with name - Myproj.Sales.Reports
    NOTE: Assume suitable parameter values for PS and PDS.
      ```
      //HRIT80A JOB 123,",", CLASS= A, MSGCLASS=A,MSGLEVEL=(0,1),NOTIFY=&SYSUID
      //STEP01 EXEC PGM=IEFBR14
      //DD0101 DD DSN=HRIT80A.MYPROJ.CUSTOMER.DETAILS,
      //          DISP=(NEW,CATLG,DELETE),
      //          SPACE=(TRK,(5,2),RLSE),
      //          VOL=SER=ZAPRD4,
      //          DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800),
      //          UNIT=SYSDA
      //STEP02 EXEC PGM=IEFBR14
      //DD0101 DD DSN=HRIT80A.MYPROJ.SALES.REPORTS,
      //          DISP=(NEW,CATLG,DELETE),
      //          SPACE=(TRK,(5,2,5),RLSE),
      //          VOL=SER=ZAPRD4,
      //          DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800),
      //          UNIT=SYSDA
      //SYSOUT DD SYSOUT=*
      ```
    
4. Write a JCL program to add below data to the existing PDS - MyProj.EMP.Details.\

      | ID  | NAME | DEPT | SALARY |
      | --- | ------ | ---- | ------ |
      | 109  | PRAMOD  | TRG | 95000 |
      | 107 | HARI  | ADM | 75000 |
      | 101 | VINAYADM | ACT | 55000 |
      | 104 | LAXMI  | ADM | 43000 |
      | 102 | AKASH  | TRG | 64000 |
      | 103 | KIRAN  | ADM | 45000 |
      | 106 | VILAS  | SLS | 67000 |
      | 105 | RAM  | SLS | 53000 |
      | 108 | ABDUL  | TRG | 38000 |
      
      STEPS: Create a PDS with name - HRIT80A.DATASET. Now add above data to its Member. Next we will use "IEBCOPY" utility to 
              copy entire member from the HRIT80A.DATASET PDS to our existing PDS with name - MYPROJ.EMP.DETAILS.\
      NOTE: IEBCOPY utility is used to copy entire member from one PDS to another PDS. It cannot be used between PS and PDS.

      ```
      //HRIT80A JOB 123,",", CLASS= A, MSGCLASS=A,MSGLEVEL=(0,1),NOTIFY=&SYSUID
      //STEP01 EXEC PGM=IEBCOPY
      //SYSPRINT DD SYSOUT=*
      //SYSIN DD DUMMY
      //SYSUT1 DD DSN=HRIT80A.DATASET,DISP=SHR
      //SYSUT2 DD DSN=HRIT80A.MYPROJ.EMP.DETAILS,
      //          DISP=(NEW,CATLG,DELETE),
      //          SPACE=(TRK,(5,2,5),RLSE),
      //          VOL=SER=ZAPRD4,
      //          DCB=(DSORG=PS,RECFM=FB,LRECL=80,BLKSIZE=800),
      //          UNIT=SYSDA
      ```
