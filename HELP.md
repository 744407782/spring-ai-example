---
title: ReAct Agent
---
flowchart TD
__START__((start))
__END__((stop))
model("model")
action_dispatcher("action_dispatcher")
execTest("execTest")
approval_threadCount("approval_threadCount")
threadCount("threadCount")
%%	condition1{"check state"}
%%	condition2{"check state"}
%%	condition3{"check state"}
__START__:::__START__ --> model:::model
%%	model:::model -.-> condition1:::condition1
%%	condition1:::condition1 -.->|continue| action_dispatcher:::action_dispatcher
model:::model -.->|continue| action_dispatcher:::action_dispatcher
%%	condition1:::condition1 -.->|end| __END__:::__END__
model:::model -.->|end| __END__:::__END__
execTest:::execTest --> action_dispatcher:::action_dispatcher
%%	approval_threadCount:::approval_threadCount -.-> condition2:::condition2
%%	condition2:::condition2 -.-> model:::model
approval_threadCount:::approval_threadCount -.-> model:::model
%%	condition2:::condition2 -.-> action_dispatcher:::action_dispatcher
approval_threadCount:::approval_threadCount -.-> action_dispatcher:::action_dispatcher
%%	condition2:::condition2 -.->|APPROVED| threadCount:::threadCount
approval_threadCount:::approval_threadCount -.->|APPROVED| threadCount:::threadCount
threadCount:::threadCount --> action_dispatcher:::action_dispatcher
%%	action_dispatcher:::action_dispatcher -.-> condition3:::condition3
%%	condition3:::condition3 -.-> model:::model
action_dispatcher:::action_dispatcher -.-> model:::model
%%	condition3:::condition3 -.-> __END__:::__END__
action_dispatcher:::action_dispatcher -.→ __END__:::__END__
%%	condition3:::condition3 -.-> execTest:::execTest
action_dispatcher:::action_dispatcher -.-> execTest:::execTest
%%	condition3:::condition3 -.-> approval_threadCount:::approval_threadCount
action_dispatcher:::action_dispatcher -.-> approval_threadCount:::approval_threadCount

	classDef __START__ fill:black,stroke-width:1px,font-size:xx-small;
	classDef __END__ fill:black,stroke-width:1px,font-size:xx-small;