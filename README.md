@startuml

start
:User Submits Order;
if (Check Warehouse Stock?) then (In Stock)
    if (Process Payment) then (Payment Success)
        if (Dispatch Order) then (Dispatch Success)
            :Show Success;
        else (Dispatch Failed)
            :Show Error;
        endif
    else (Payment Failed)
        :Show Error;
    endif
else (No Stock)
    :Show Error;
endif

stop

@enduml


flowchart TB
   Start --> USO;
   USO(User Submits Order) --> CWS;
   CWS(Check Warehouse Stock) -->|In Stock| PP
   CWS -->|No Stock| SE
   SE(Show Error) --> Finished
   PP(Process Payment) -->|Payment Success| DO
   PP -->|Payment Failed| SE
   DO(Dispatch Order) --> |Dispatch Success| SS
   DO -->|Dispatch Failed| SE
   SS(Show Success) --> Finished   
