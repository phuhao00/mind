
### 地图服

```golang 
type MapServer struct {
    ScenceManager 
    UserManager
    BuffManager

}

type ScenceManager struct {

    allScences map[zoneServerId]map[scenceId]scence

}

```