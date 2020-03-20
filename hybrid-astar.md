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

	-->hybridA*算法
		->updateH(...)更新H值
		->start点加入开放列表open
		->nodes3D在对应索引iPred存放start点
		->以下循环执行.......
		->从open sets中找出代价最低的点,并记录迭代次数iterations
		->判断状态，如果是close则剔除，执行上一步
		->判断状态，是open则还没进行扩展
			->首先标记为close状态,从open sets里剔除该点
			->如果到达终点或满足迭代上限，则返回nodes3D节点
			->非终点，满足dubin条件
				->---------
			->hybrid A*搜索，从6个方向搜索
				->---------
				

	-->A*算法
		->start.updateH(goal) 更新起点的H值
		->start点加入开放列表open
		->nodes2D在对应索引iPred存放start点
		->以下循环执行.......
		->从open sets中找出代价最低的点
		->判断状态，如果是close则剔除，执行上一步
		->判断状态，是open则还没进行扩展
			->首先标记为close状态,再标记为discover()已搜索状态,从open sets里剔除该点
			->如果到达终点，则返回G值
			->非终点，从八个方向寻找
				->createSuccessor依次查找8个近邻点
					->继承当前点的g值
					->x+=dx, y+=dy
				->updateG:从起点到现在的移动代价，g += movementCost(*pred) 原g值再加上移动的代价
				->movementCost:移动代价为 sqrt(deltax^2 + deltay^2)
				->updateH:从现在到终点的移动代价，h = movementCost(goal)
				
		






