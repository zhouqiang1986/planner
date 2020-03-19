	->HybridAStar::Constants::cellSize = 1	
	->HybridAStar::Constants::manual = true
	
	-> astar->rviz
		-> /move_base_simple/start
		
	-> rviz->astar
		-> /move_base_simple/goal 调用setGoal函数
		-> /initialpose 调用setStart函数
	-> map_server->astar
		-> /map 调用setMap函数
	-> map_server->rviz
		-> /map 调用setMap函数


	-->setMap回调函数
		->CollisionDetection.updateGrid碰撞检测更新地图
		->栅格地图转换为二值地图binMap
		->voronoiDiagram

	-->setStart回调函数
		->接收在rviz设定的起点，再pub给rviz rviz map坐标为:右为x，前为y 航向从x开始逆时针转0~360度 
		->validStart=true 合法的起点标志置true

	-->setGoal回调函数
		->接收在rviz设定的终点
		->validGoal=true 合法的终点标志置true
		->plan()执行规划函数

	-->plan()
		->Node3D start和goal点创建3D地图
		->Node2D 创建2D地图
		






