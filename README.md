# utl-flag-three-or-more-of-the-same-value
Flag three or more of the same value
    Flag three or more of the same value                                                                             
                                                                                                                     
    github                                                                                                           
    https://tinyurl.com/yddspr5c                                                                                     
    https://github.com/rogerjdeangelis/utl-flag-three-or-more-of-the-same-value                                      
                                                                                                                     
    SAS Forum                                                                                                        
    https://tinyurl.com/yb9mp84c                                                                                     
    https://communities.sas.com/t5/SAS-Programming/IF-THEN-statement-for-a-combination-of-variables/m-p/519722       
                                                                                                                     
    Novinosrin                                                                                                       
    https://communities.sas.com/t5/user/viewprofilepage/user-id/138205                                               
                          4                                                                                          
                                                                                                                     
    INPUT                                                                                                            
    =====                                                                                                            
                              | RULES                                                                                
     WORK.HAVE total obs=6    |                                                                                      
                              |                                                                                      
       V1    V2    V3    V4   | Flg                                                                                  
                              |                                                                                      
        1     1     3     1   |  1    * three 1s                                                                     
        9     3     9     9   |  1    * three 9s                                                                     
        1     1     2     2   |  0                                                                                   
        1     3     2     4   |  0                                                                                   
        2     3     1     4   |  0                                                                                   
        1     2     1     3   |  0                                                                                   
                                                                                                                     
                                                                                                                     
    EXAMPLE OUTPUT                                                                                                   
    --------------                                                                                                   
                                                                                                                     
     WORK.WANT total obs=6                                                                                           
                                                                                                                     
      V1    V2    V3    V4    FLG                                                                                    
                                                                                                                     
       1     1     1     3     1                                                                                     
       1     1     1     3     1                                                                                     
       1     1     2     2     0                                                                                     
       1     2     3     4     0                                                                                     
       1     2     3     4     0                                                                                     
       1     1     2     3     0                                                                                     
                                                                                                                     
                                                                                                                     
    PROCESS                                                                                                          
    =======                                                                                                          
                                                                                                                     
    data want;                                                                                                       
       set have;                                                                                                     
       array v v:;                                                                                                   
       i_=1;                                                                                                         
       call sortn(of v1-v4);                                                                                         
       flg=0;                                                                                                        
       do i=2 to dim(v);                                                                                             
          if v(i)=v(i-1) then i_=sum(i_,1);                                                                          
          else i_=1;                                                                                                 
          if i_=3 then do;                                                                                           
             flg=v(i);                                                                                               
             leave;                                                                                                  
          end;                                                                                                       
       end;                                                                                                          
       drop i:;                                                                                                      
    run;quit;                                                                                                        
                                                                                                                     
    *                _              _       _                                                                        
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                                 
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                                
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                                
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                                
                                                                                                                     
    ;                                                                                                                
                                                                                                                     
    data have;                                                                                                       
      input v1 v2 v3 v4;                                                                                             
    cards;                                                                                                           
    1 1 3 1                                                                                                          
    1 3 1 1                                                                                                          
    1 1 2 2                                                                                                          
    1 3 2 4                                                                                                          
    2 3 1 4                                                                                                          
    1 2 1 3                                                                                                          
    ;;;;                                                                                                             
    run;quit;                                                                                                        
                                                                                                                     
                                                                                                                     
