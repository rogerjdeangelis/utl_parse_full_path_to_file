# utl_parse_full_path_to_file
Given a full path extract the folder, file name and filename with extension.   Four Solutions    1. macro variable 'fill_path';   2. datastep  'full path';   3. datastep  FCMP;   4. datastep  DOSUBL;

    ```  Given a full path extract the folder, file name and filename with extension.                                                                                 ```
    ```                                                                                                                                                               ```
    ```   Four Solutions                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```    1. macro variable 'fill_path';                                                                                                                             ```
    ```    2. datastep  'full path';                                                                                                                                  ```
    ```    3. datastep  FCMP;                                                                                                                                         ```
    ```    4. datastep  DOSUBL;                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```    (some of these solutions predate scan enhancements, ie 'call scan, neg scanning'.                                                                          ```
    ```                                                                                                                                                               ```
    ```   *                                                                                                                                                           ```
    ```   _ __   __ _ _ __ ___  ___   _ __ ___   __ _  ___ _ __ ___   __   ____ _ _ __                                                                                ```
    ```  | '_ \ / _` | '__/ __|/ _ \ | '_ ` _ \ / _` |/ __| '__/ _ \  \ \ / / _` | '__|                                                                               ```
    ```  | |_) | (_| | |  \__ \  __/ | | | | | | (_| | (__| | | (_) |  \ V / (_| | |                                                                                  ```
    ```  | .__/ \__,_|_|  |___/\___| |_| |_| |_|\__,_|\___|_|  \___/    \_/ \__,_|_|                                                                                  ```
    ```  |_|                                                                                                                                                          ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```    %let full_path=d:/sd1/utl_class.sas7bdat;                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    mGetFileNoExt      * get file without extention   ==> utl_class                                                                                            ```
    ```    mGetFileWithExt    * get file with extention      ==> utl_class.sas7bdate                                                                                  ```
    ```    mGetFolder         * get folder stem              ==> d:/sd1/                                                                                              ```
    ```                                                                                                                                                               ```
    ```     Test cases                                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```      %let full_path=d:/sd1/utl_class.sas7bdat;                                                                                                                ```
    ```                                                                                                                                                               ```
    ```      %put %mGetFileNoExt  (&full_path);                                                                                                                       ```
    ```      %put %mGetFileWithExt(&full_path);                                                                                                                       ```
    ```      %put %mgetFolder     (&full_path);                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      %macro mGetFileNoExt(pth)/des="macro variable get file name without extention";                                                                          ```
    ```         %qscan(&pth,-2,%str(./\))                                                                                                                             ```
    ```       %mend mGetFileNoExt;                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```      %macro mGetFileWithExt(pth)/des="macro variable get file name without extention";                                                                        ```
    ```         %qscan(&pth,-1,%str(/\))                                                                                                                              ```
    ```      %mend mGetFileWithExt;                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```      %macro mgetFolder(pth)/des="macro variable get folder name";                                                                                             ```
    ```         %let revstr=%qleft(%qsysfunc(reverse(&pth)));                                                                                                         ```
    ```         %let cutstr=%qsubstr(&revstr,%qsysfunc(indexc(&revstr,%str(/\))));                                                                                    ```
    ```         %let gotstm=%qleft(%qsysfunc(reverse(&cutstr)));                                                                                                      ```
    ```         %str(&gotstm)                                                                                                                                         ```
    ```      %mend mgetFolder;                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  *                                _       _                                                                                                                   ```
    ```   _ __   __ _ _ __ ___  ___    __| | __ _| |_ __ _  __   ____ _ _ __                                                                                          ```
    ```  | '_ \ / _` | '__/ __|/ _ \  / _` |/ _` | __/ _` | \ \ / / _` | '__|                                                                                         ```
    ```  | |_) | (_| | |  \__ \  __/ | (_| | (_| | || (_| |  \ V / (_| | |                                                                                            ```
    ```  | .__/ \__,_|_|  |___/\___|  \__,_|\__,_|\__\__,_|   \_/ \__,_|_|                                                                                            ```
    ```  |_|                                                                                                                                                          ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```    %getFileNoExt      * get file without extention   ==> utl_class                                                                                            ```
    ```    %getFileWithExt    * get file with extention      ==> utl_class.sas7bdate                                                                                  ```
    ```    %getFolder         * get folder stem              ==> d:/sd1/                                                                                              ```
    ```                                                                                                                                                               ```
    ```    data _null_;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      full_path="d:/sd1/utl_class.sas7bdat";                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```      getFileNoExt   =  %getFileNoExt  (full_path);                                                                                                            ```
    ```      getFileWithExt =  %getFileWithExt(full_path);                                                                                                            ```
    ```      getFolder      =  %getFolder     (full_path);                                                                                                            ```
    ```                                                                                                                                                               ```
    ```      put (_all_) (= $ /);                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```    run;quit;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    FULL_PATH      = d:/sd1/utl_class.sas7bdat                                                                                                                 ```
    ```    GETFILENOEXT   = utl_class                                                                                                                                 ```
    ```    GETFILEWITHEXT = utl_class.sas7bdat                                                                                                                        ```
    ```    GETFOLDER      = utl_class.sas7bdat                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```      %macro getFileNoExt(pth)/des="datastep variable get file name without extention";                                                                        ```
    ```         scan(full_path,-2,"./\")                                                                                                                              ```
    ```       %mend getFileNoExt;                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      %macro getFileWithExt(pth)/des="datastep variable get file name without extention";                                                                      ```
    ```         scan(full_path,-1,"/\")                                                                                                                               ```
    ```      %mend GetFileWithExt;                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      %macro getFolder(pth)/des="macro variable get folder name";                                                                                              ```
    ```       left(reverse(left(scan(reverse(full_path),1,"/\"))))                                                                                                    ```
    ```      %mend getFolder;                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  * __                                                                                                                                                         ```
    ```   / _| ___ _ __ ___  _ __                                                                                                                                     ```
    ```  | |_ / __| '_ ` _ \| '_ \                                                                                                                                    ```
    ```  |  _| (__| | | | | | |_) |                                                                                                                                   ```
    ```  |_|  \___|_| |_| |_| .__/                                                                                                                                    ```
    ```                     |_|                                                                                                                                       ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```    getFileNoExt      * get file without extention   ==> utl_class                                                                                             ```
    ```    getFileWithExt    * get file with extention      ==> utl_class.sas7bdate                                                                                   ```
    ```    getFolder         * get folder stem              ==> d:/sd1/                                                                                               ```
    ```                                                                                                                                                               ```
    ```    data _null_;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      full_path="d:/sd1/utl_class.sas7bdat";                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```      getFileNoExt   =  getFileNoExt  (full_path);                                                                                                             ```
    ```      getFileWithExt =  getFileWithExt(full_path);                                                                                                             ```
    ```      getFolder      =  getFolder     (full_path);                                                                                                             ```
    ```                                                                                                                                                               ```
    ```      put (_all_) (= $ /);                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```    run;quit;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    FULL_PATH      = d:/sd1/utl_class.sas7bdat                                                                                                                 ```
    ```    GETFILENOEXT   = utl_class                                                                                                                                 ```
    ```    GETFILEWITHEXT = utl_class.sas7bdat                                                                                                                        ```
    ```    GETFOLDER      = utl_class.sas7bdat                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  options cmplib=work.funcs;                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  proc fcmp outlib=work.funcs.parsepath;                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```    function getFolder(expr $) $200;                                                                                                                           ```
    ```      length result $200;                                                                                                                                      ```
    ```      result=left(reverse(left(scan(reverse(expr),1,"/\"))));                                                                                                  ```
    ```      return(result);                                                                                                                                          ```
    ```    endsub;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```    function getFileNoExt(expr $) $200;                                                                                                                        ```
    ```      length result $200;                                                                                                                                      ```
    ```      result=scan(expr,-2,"./\");                                                                                                                              ```
    ```      return(result);                                                                                                                                          ```
    ```    endsub;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```    function getFileWithExt(expr $) $200;                                                                                                                      ```
    ```      length result $200;                                                                                                                                      ```
    ```      result=left(reverse(left(scan(reverse(full_path),1,"/\"))));                                                                                             ```
    ```      return(result);                                                                                                                                          ```
    ```    endsub;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  run;                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  *    _                 _     _                                                                                                                               ```
    ```    __| | ___  ___ _   _| |__ | |                                                                                                                              ```
    ```   / _` |/ _ \/ __| | | | '_ \| |                                                                                                                              ```
    ```  | (_| | (_) \__ \ |_| | |_) | |                                                                                                                              ```
    ```   \__,_|\___/|___/\__,_|_.__/|_|                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```    getFileNoExt      * get file without extention   ==> utl_class                                                                                             ```
    ```    getFileWithExt    * get file with extention      ==> utl_class.sas7bdate                                                                                   ```
    ```    getFolder         * get folder stem              ==> d:/sd1/                                                                                               ```
    ```                                                                                                                                                               ```
    ```    %symdel file /nowarn;                                                                                                                                      ```
    ```    data _null_;                                                                                                                                               ```
    ```      length file $32;                                                                                                                                         ```
    ```      full_path="d:/sd1/utl_class.sas7bdat";                                                                                                                   ```
    ```      call symputx('full_path',full_path);                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      * flexible - you can use fcmp, macro or datastep code;                                                                                                   ```
    ```      file=dosubl('                                                                                                                                            ```
    ```        %let file=%sysfunc(getFileNoExt  (&full_path)));                                                                                                       ```
    ```        %put &=full_path;                                                                                                                                      ```
    ```        /* more code datasteps or procedures */                                                                                                                ```
    ```        ');                                                                                                                                                    ```
    ```      file=symget("file");                                                                                                                                     ```
    ```      put (_all_) (= $ /);                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```    run;quit;                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```    %symdel file /nowarn;                                                                                                                                      ```
    ```    data _null_;                                                                                                                                               ```
    ```      length file $32;                                                                                                                                         ```
    ```      full_path="d:/sd1/utl_class.sas7bdat";                                                                                                                   ```
    ```      call symputx('full_path',full_path);                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      * flexible - you can use fcmp, macro or datastep code;                                                                                                   ```
    ```      file=dosubl('                                                                                                                                            ```
    ```        data _null_;                                                                                                                                           ```
    ```           file=getFileNoExt(symget("full_path"));                                                                                                             ```
    ```           call symputx("file",file);                                                                                                                          ```
    ```        run;quit;                                                                                                                                              ```
    ```        /* more code datasteps or procedures */                                                                                                                ```
    ```        ');                                                                                                                                                    ```
    ```      file=symget("file");                                                                                                                                     ```
    ```      put (_all_) (= $ /);                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```    run;quit;
