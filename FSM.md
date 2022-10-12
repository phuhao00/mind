
### 状态机

```golang 
type FSM struct {
    initState 
    curState
    isRun
    triggerTrans map[trigger]map[fromState]toState
    activeController
    passiveController
}

func (f *FSM)Run(time.Time){

    if f.activeController!=nil&&f.activeController.Ready(){
        f.activeController.Process()
        return
    }
    
    if f.passiveController!=nil&&f.passiveController.Ready(){
        f.passiveController.Process()
        return
    }

}

func (f *FSM)OnTrigger(t trigger){
    if pair,ok:=f.triggerTrans[t];ok{
        if toState,ok:=pair[f.curState];ok {
            f.curState.Leave()
            f.curState=toState
            toState.Enter(time.Now())
        }
    }

}

type State interface {
    Name() string
    Enter(t time.Time)
    Check(t time.Time)
    Execute(t time.Time)
    Leave()
}
```