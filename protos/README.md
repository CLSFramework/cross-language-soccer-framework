# Environment Messages
## State
this message contains 3 property:

- ```agent_type```: Indicates the type of the connected agent whether it is player, coach, or trainer. The value can be ```PlayerT```, ```CoachT```, and ```TrainerT``` that shows. 
- ```world_model```: contains the information of the field environment that the agent recevied from the RCSSServer and parsed by the helios-base. More information is provided in the [WorldModel](#WorldModel) section. 
- ```full_world_model```: contains the information of the field environment that the agent recevied from the RCSSServer and parsed by the helios-base. More information is provided in the [WorldModel](#WorldModel) section.  

the difference between ```world_model``` and the ```full_world_model``` is that the ```full_world_model``` contains the information of all the objects in the field, while the ```world_model``` contains the information of the objects that are in the agent's view. Note that the ```world_model``` information is noisy and may not be accurate while the ```full_world_model``` is accurate.

In the defualt config of the RCSSServer, the agent only recieves the ```world_model``` information; however, by changing the config file, the agent can recieve the ```full_world_model``` information too. Although the agent revieves the ```full_world_model``` information, the full state data will be stored in the ```world_model``` property. To recieve both ```world_model``` and ```full_world_model``` information, the agent should change the ```player.conf``` file in the proxy base. 
```
TODO the property of the player.conf for recieving the full_world_model
```

### WorldModel
The ```WorldModel``` type contains the following information:
- ```intercept_table```: Contains the data of the important players that can intercept the ball.In [here](#InterceptTable) we explain more about this data. 
- ```our_team_name```: The name of the team that the agent is playing for.
- ```their_team_name```: The name of the opponent team.
- ```our_side```: The side of the field that the agent is playing for. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN```.
- ```last_set_play_start_time```: The time that the last set play (Game Type) started. 
- ```self```: The information of the agent itself, such as the uniform number, the position, the velocity, etc. In the [Self](#Self) section, we explain more about this data.
- ```ball```: The information of the ball, such as the position, the velocity, etc. In the [Ball](#Ball) section, we explain more about this data.
- ```teammates```*: This property is a list of the ```Players``` that contains the information of the teammates. In the [Player](#Player) section, we explain more about this data.
- ```opponents```*: This property is a list of the ```Players``` that contains the information of the opponents. In the [Player](#Player) section, we explain more about this data.
- ```unknowns```: This property is a list of the ```Players``` that contains the information of the unknown players. Unknown players are the ones that the agent did not receive any information about the uniform number and the side of them. In the [Player](#Player) section, we explain more about this data.
- ```our_players_dict```*: This property is a dictionary that contains the information of the teammates. The key of the dictionary is the uniform number of the player. Note that if the agent does not have any data about a player, the player will not be in the dictionary (check for the null). In the [Player](#Player) section, we explain more about this data.
- ```their_players_dict```*: This property is a dictionary that contains the information of the opponents. The key of the dictionary is the uniform number of the player. Note that if the agent does not have any data about a player, the player will not be in the dictionary (check for the null). In the [Player](#Player) section, we explain more about this data.
- ```our_goalie_uniform_number```: The uniform number of the goalie of the agent's team.
- ```their_goalie_uniform_number```: The uniform number of the goalie of the opponent's team.
- ```offside_line_x```: The x position of the offside line.
- ```ofside_line_x_count```: The number of cycles that passed of the offside line calculation.
- ```kickable_teammate_id```: The uniform number of the teammate that the agent can kick the ball to.
- ```kickable_opponent_id```: The uniform number of the opponent that the agent can kick the ball to.
- ```last_kick_side```: The side that the last kick was done. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN```.
- ```last_kicker_uniform_number```: The uniform number of the player that kicked the ball last time.
- ```cycle```: The current cycle of the game.
- ```stoped_cycle```: The cycle that the game stopped. The stopped cycle increase when the game cycle is not updated. This happens when the games stops for some game modes.
- ```game_mode_type```: The current mode of the game. This value can be ```PlayOn```, ```BeforeKickOff```, etc. We will explain more about this in the [GameModeType](#GameModeType) section.
- ```left_team_score```: The score of the left team.
- ```right_team_score```: The score of the right team.
- ```is_our_set_play```: Indicates whether the agent's team is in the set play mode. It means if the agent's team should kick the ball for the current game mode.
- ```is_their_set_play```: Indicates whether the opponent's team is in the set play mode. It means if the opponent's team should kick the ball for the current game mode.
- ```our_team_score```: The score of the agent's team.
- ```their_team_score```: The score of the opponent's team.
- ```is_penalty_kick_mode```: Indicates whether the game is in the penalty kick mode.
- ```helios_home_positions```: The position of the players based on the defined formations in the ```src/formtaions-dt``` directory. The position of the players is calculated based on the position of the ball and the formation of the team. This position is calculated by the base and is stored in this dictionary. The key of the dictionary is the uniform number of the player and the value is the position of the player.

*: TODO

#### InterceptTable
The ```InterceptTable``` type contains the following information:
- ```self_reach_steps```: The number of cycles that the agent can reach the ball.
- ```first_teammate_reach_steps```: The number of cycles that the first teammate can reach the ball. Note that the agent is not considered as a teammate.
- ```second_teammate_reach_steps```: The number of cycles that the second teammate can reach the ball. Note that the agent is not considered as a teammate.
- ```first_opponent_reach_steps```: The number of cycles that the first opponent can reach the ball.
- ```second_opponent_reach_steps```: The number of cycles that the second opponent can reach the ball.
- ```first_teammate_id```: The uniform number of the first teammate that can intercept the ball.
- ```second_teammate_id```: The uniform number of the second teammate that can intercept the ball.
- ```first_opponent_id```: The uniform number of the first opponent that can intercept the ball.
- ```second_opponent_id```: The uniform number of the second opponent that can intercept the ball.
- ```self_intercept_info```: TODO?!

#### Self
The ```Self``` type contains the following information:
- ```position```: The position of the agent.
- ```seen_position```: The position of the agent that the agent saw.
- ```heard_position```: The position of the agent that the agent heard.
- ```velocity```: The velocity of the agent.
- ```seen_velocity```: The velocity of the agent that the agent saw.
- ```pos_count```: The number of cycles that passed since the agent's position was updated.
- ```seen_pos_count```: The number of cycles that passed since the agent's seen position was updated. TODO ?!(Correct?)
- ```heard_pos_count```: The number of cycles that passed since the agent's heard position was updated. TODO ?!(Correct?)
- ```vel_count```: The number of cycles that passed since the agent's velocity was updated.
- ```seen_vel_count```: The number of cycles that passed since the agent's seen velocity was updated. TODO ?!(Correct?)
- ```ghost_count```: TODO ?!
- ```id```: TODO?!
- ```side```: The side of the agent. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN``.
- ```uniform_number```: The uniform number of the agent.
- ```uniform_number_count```: The number of cycles that passed since the agent's uniform number was updated.
- ```is_goalie```: Indicates whether the agent is the goalie of the team.
- ```body_direction```: The direction of the agent's body.
- ```body_direction_count```: The number of cycles that passed since the agent's body direction was updated.
- ```face_direction```: The direction of the agent's face. This value is the direction that the agent is looking at and it is global, not relative to the player's body.
- ```face_direction_count```: The number of cycles that passed since the agent's face direction was updated.
- ```point_to_direction```: The direction that the agent is pointing to. Check the [PointToDirection](#PointToDirection) section for more information.
- ```point_to_direction_count```: The number of cycles that passed since the agent's point to direction was updated.
- ```is_kicking```: Indicates whether the agent is kicking the ball.
- ```dist_from_ball```: The distance of the agent from the ball.
- ```angle_from_ball```: The angle of the agent from the ball. This value is relative to the agent's body. (TODO CHECK)
- ```ball_reach_steps```: The number of cycles that the agent can reach the ball.
- ```is_tackling```: Indicates whether the agent is tackling.
- ```relative_neck_direction```: The direction of the agent's neck relative to the agent's body. It's the value of the face direction relative to the body direction.
- ```stamina```: The stamina of the agent.
- ```is_kickable```: Indicates whether the agent can kick the ball.
- ```catch_probability```: The probability of the agent to catch the ball. Catching the ball is for the goalie.
- ```tackle_probability```: The probability of the agent to tackle the opponent. (TODO CHECK)
- ```foul_probability```: The probability of the agent to foul the opponent while tackling. (TODO CHECK)
- ```view_width```: The width of the agent's view. This value can be ```NARROW```, ```NORMAL```, or ```WIDE``.
- ```type_id```: The player type id of the agent. This value is explained in the [PlayerType](#PlayerType) section.
- ```kick_rate```: The rate of the agent to kick the ball. This value is calculated based on the player type and the position of the ball relative to the agent's position and body.

#### Player
The ```Player``` type contains the following information:
- ```position```: The position of the player.
- ```seen_position```: The position of the player that the agent saw.
- ```heard_position```: The position of the player that the agent heard.
- ```velocity```: The velocity of the player.
- ```seen_velocity```: The velocity of the player that the agent saw.
- ```pos_count```: The number of cycles that passed since the player's position was updated.
- ```seen_pos_count```: The number of cycles that passed since the player's seen position was updated. TODO ?!(Correct?)
- ```heard_pos_count```: The number of cycles that passed since the player's heard position was updated. TODO ?!(Correct?)
- ```vel_count```: The number of cycles that passed since the player's velocity was updated.
- ```seen_vel_count```: The number of cycles that passed since the player's seen velocity was updated. TODO ?!(Correct?)
- ```ghost_count```: TODO ?!
- ```dist_from_self```: The distance of the player from the agent.
- ```angle_from_self```: The angle of the player from the agent. This value is relative to the agent's body. (TODO CHECK)
- ```id```: TODO?!
- ```side```: The side of the player. The value can be ```LEFT```, ```RIGHT```, or ```UNKNOWN``.
- ```uniform_number```: The uniform number of the player.
- ```uniform_number_count```: The number of cycles that passed since the player's uniform number was updated.
- ```is_goalie```: Indicates whether the player is the goalie of the team.
- ```body_direction```: The direction of the player's body.
- ```body_direction_count```: The number of cycles that passed since the player's body direction was updated.
- ```face_direction```: The direction of the player's face. This value is the direction that the player is looking at and it is global, not relative to the player's body.
- ```face_direction_count```: The number of cycles that passed since the player's face direction was updated.
- ```point_to_direction```: The direction that the player is pointing to. Check the [PointToDirection](#PointToDirection) section for more information.
- ```point_to_direction_count```: The number of cycles that passed since the player's point to direction was updated.
- ```is_kicking```: Indicates whether the player is kicking the ball.
- ```dist_from_ball```: The distance of the player from the ball.
- ```angle_from_ball```: The angle of the player from the ball. This value is relative to the player's body. (TODO CHECK)
- ```ball_reach_steps```: The number of cycles that the player can reach the ball.
- ```is_tackling```: Indicates whether the player is tackling.
- ```type_id```: The player type id of the player. This value is explained in the [PlayerType](#PlayerType) section.

#### GameModeType
The ```GameModeType``` is an enum that contains the following values:
- ```BeforeKickOff```: The game mode that the game is before the kick-off.
- ```TimeOver```: The game mode that the time is over. (TODO CHECK)
- ```PlayOn```: The game mode that the game is playing.
- ```KickOff_```: The game mode that the game is in the kick-off mode.
- ```KickIn_```: The game mode that the game is in the kick-in mode.
- ```FreeKick_```: The game mode that the game is in the free-kick mode.
- ```CornerKick_```: The game mode that the game is in the corner-kick mode.
- ```GoalKick_```: The game mode that the game is in the goal-kick mode. (TODO CHECK?)
- ```AfterGoal_```: The game mode that the game is after the goal.
- ```OffSide_```: The game mode that the game is in the offside mode.
- ```PenaltyKick_```: The game mode that the game is in the penalty-kick mode.
- ```FirstHalfOver```: The game mode that the first half is over.
- ```Pause```: The game mode that the game is paused. (TODO CHECK)
- ```Human```: The game mode that the game is in the human mode. (TODO CHECK)
- ```FoulCharge_```: The game mode that the game is in the foul-charge mode.
- ```FoulPush_``` TODO
- ```FoulMultipleAttacker_```
- ```FoulBallOut_```
- ```BackPass_```
- ```FreeKickFault_```
- ```CatchFault_```
- ```IndFreeKick_```
- ```PenaltySetup_```
- ```PenaltyReady_```
- ```PenaltyTaken_```
- ```PenaltyMiss_```
- ```PenaltyScore_```
- ```IllegalDefense_```
- ```PenaltyOnfield_```
- ```PenaltyFoul_```
- ```GoalieCatch_```
- ```ExtendHalf```
- ```MODE_MAX```


# Agent Actions
After receiving the State message, the agent should send a list of actions to the base so the base can execute them and send them to the RCSSServer. The ```PlayerActions``` message contains a list of [```Action```](#Action). 

This list should only contains one Body Action and several other actions. By Body Action, we mean the actions that are related to the agent's body, such as ```Dash```, ```Turn```, ```Kick```, ```Tackle```, ```Catch```, and ```Move```. The agent can only do these actions once in a cycle. The other actions, such as ```TurnNeck```, ```ChangeView```, ```Say```, ```PointTo```, and ```AttentionTo``` can be done multiple times in a cycle. The agent can only do each type of action once in a cycle. For example, the agent can only do one ```Dash``` action in a cycle, while it can ```ChangeView```, ```Say```, and ```TurnNeck``` in that cycle. Note that the agent cannot do the second type actions more than once in a cycle.

In addition to that, the agent can send the some debug actions to the base. These actions are ```Log``` and ```DebugClient```. These actions are useful when you are using the [soccerwindow2](https://github.com/helios-base/soccerwindow2) as the monitor. These actions are for the debug tools of this application.

## Action Levels
Helios-base and the Proxy base has two different level of actions which are Low-Level Actions and High-Level Actions.

- Low-Level Actions: These actions are the ones that RCSSServer will receive them from the agents to apply them on the players. These actions are the actions that are related to the agent's situation and needs many calculations to do a simple task, such as moving to a point or kicking the ball to a certain target.
- High-Level Actions: These actions are developed in the helios-base and also the Proxy base supports them. These actions are very simple to use and let the developer consentrate on the strategy and the decision making of the agent. For instance, the agent can send a ```Body_GoToPoint``` action to the base and the base will calculate the best way to move the agent to the target point. ```Body_GoToPoint``` is a high-level action that finds the most optimized way of turning and dashing for the agent to reach the target point.

in the folliwng sections, we will explain both type of the actions that the agent can send to the base.

## Low-Level Actions
### Dash
This action gets two parameters:
- ```power``` (float): The power of the dash. The value can be between ```ServerParam.max_power``` and ```ServerParam.min_param```.
- ```relative_direction``` (float): The direction of the dash which is relative to the body of the agent. The value can be between ```-180``` and ```180```.

The dash action is most effective with the angles of ```0``` and ```180``` (back dash), and in the other directions it will reduced based on the angle.

The maximum speed of the player is dependent on the agent's [```player_type```](#Playertype).


### Turn
This action gets one parameter:
- ```relative_direction``` (float): The direction of the turn which is relative to the body of the agent. The value can be between ```-180``` and ```180```. Note that maximum value for the turn is related to the agent's ```speed```, and [```player_type```](#Playertype).

### Kick
This action gets two parameters:
- ```power``` (float): The power of the kick. The value can be between ```ServerParam.max_power``` and ```ServerParam.min_param```.
- ```relative_direction``` (float): The direction of the kick which is relative to the body of the agent. The value can be between ```-180``` and ```180```.

The speed of the ball after the kick action is calculated based on the relative position of the ball and the agent and also it is related to the ```kick_rate``` of the agent which is in [```player_type```](#Playertype).

### Tackle
This action gets two parameter:
- ```power_or_dir``` (float): (TODO CHECK)
- ```foul``` (float): (TODO CHECK)

### Catch
This action gets no parameter, and only the goalie can use this action. If the ball is within the catchable area of the agent, the agent catchs the ball with some probabilty. The probability of catching the ball and the catchable area is related to the agent's [```player_type```](#Playertype).

### Move
This action gets two parameters:
- ```x``` (float): The x position of the target point.
- ```y``` (float): The y position of the target point.

This actions is only used in the ```BeforeKickOff``` mode. The agent can move to the target point with the ```Move``` action.

### TurnNeck
This action gets one parameter:
- ```moment``` (float): The current angle of the agent's neck will be added to this value. The value can be between ```ServerParam.max_neck_moment``` and ```ServerParam.min_neck_moment```.

The maximum and the minimum agent's neck angle are ```ServerParam.max_neck_angle``` and ```ServerParam.min_neck_angle```.

The neck angle is the angle of the view area of the agent.

### ChangeView
This action gets one parameter:
- ```width``` (ViewWidth): The width of the agent's view. The value can be ```NARROW```, ```NORMAL```, or ```WIDE```.

The ```NARROW``` view is 60 degrees, the ```NORMAL``` view is 120 degrees, and the ```WIDE``` view is 180 degrees.
Also with the ```NARROW``` view, the agent can see each cycle; however, with the ```NORMAL``` view, the agent can see every two cycles, and with the ```WIDE``` view, the agent can see every three cycles.

### PointTo
This action gets two parameter:
- ```x``` (float): The x position of the target point.
- ```y``` (float): The y position of the target point.

This action is used to point to a target point. Other players can see the direction of the point. This helps the team for more communications.

This action has timeout which the agent has to wait for the timeout to finish before sending another ```PointTo``` action.

### PointToOf
This action gets no parameter. This action is used to remove the pointing of the agent.

### AttentionTo
This action gets two parameter:
- ```side``` (Side): The side of the player that the agent wants to pay attention to. The value can be ```LEFT```, ```RIGHT```.
- ```uniform_number``` (int): The uniform number of the player that the agent wants to pay attention to.

This action is used to pay attention to a player which the agent hears the messages that the player says. A player can attention to maximum of ```ServerParam.player_hear_max``` players.

### AttentionToOf
This action gets no parameter. This action is used to remove the attention of the agent.


## high-Level Actions
### Body_GoToPoint
This action gets three parameter:
- ```target_point``` (```Vector2D```): The target point that the agent wants to move to.
- ```distance_threshold``` (float): The distance threshold that the agent should reach to the target point.
- ```max_dash_power``` (float): The maximum dash power that the agent can use to move to the target point.

This action is used to move the agent to the target point. The agent will calculate the best way to move to the target point and will send the [```Dash```](#Dash) and [```Turn```](#Turn) actions to the base.

Since the position of the agent that is calculated based on the agent's observation is noisy, the ```distance_threshold``` is used to check if the agent is close enough to the target point. If the agent is close enough to the target point, the agent will stop moving. If the ```distance_threshold``` is ```0```, the agent will ```Dash``` and ```Turn``` around the ```target_point``` and it never stops. This might cause the stamina of the agent to be reduced quickly.

### Body_SmartKick
This action gets four parameter:
- ```target_point``` (```Vector2D```): The target point that the agent wants to kick the ball to.
- ```first_speed``` (float): The first speed that the agent wants to kick the ball with.
- ```first_speed_threshold``` (float): The threshold of the first speed must be at least.
- ```max_steps``` (int): The maximum number of steps that the agent can kick the ball. (Maximum is 3)

This action is used to kick the ball to the target point. The agent will calculate the best way to kick the ball to the target point and will send the [```Kick```](#Kick) action to the base.

The ```first_speed``` is the speed that this action will try to reach; however, the agent trys to kick the ball with the maximum speed that the agent can kick the ball. The ```first_speed_threshold``` is the minimum speed that the agent should kick the ball with. If the agent cannot kick the ball with the ```first_speed_threshold```, the agent will not kick the ball.

The ```max_steps``` is the maximum number of steps that the agent can kick the ball. The agent will try to kick the ball with the minimum number of steps. As the ```first_speed``` more stpes will be used to kick the ball. The maximum number of steps is 3.

The maximum speed of the ball is ```ServerParam.ball_speed_max``` which is almost ```3```.

### Bhv_BeforeKickOff
This action gets one parameter:
- ```point``` (```Vector2D```): The target point that the agent wants to move to.

This action is used for the agent to move to the target point in the ```BeforeKickOff``` mode.

### Bhv_BodyNeckToBall
This action gets no parameter. This action is used to change the neck direction of the agent to the ball. If it is not possible to see the ball, the agent will turn to the ball.

If the agent's position is not valid, the agent scans the field to find position of itself and the ball by turning around itself.

### Bhv_BodyNeckToPoint
This action gets one parameter:
- ```point``` (```Vector2D```): The target point that the agent wants to move to.

This action is used to change the neck direction of the agent to the target point. If it is not possible to see the target point, the agent will turn to the target point. If the agent's position is not valid, the agent scans the field to find position of itself by turning around itself.

### Bhv_Emergency
This action gets no parameter. This action is used to scan the field by turning around itself.

### Bhv_GoToPointLookBall
This action gets three parameter:
- ```target_point``` (```Vector2D```): The target point that the agent wants to move to.
- ```distance_threshold``` (float): The distance threshold that the agent should reach to the target point.
- ```max_dash_power``` (float): The maximum dash power that the agent can use to move to the target point.

This action is as same as the [```Body_GoToPoint```](#Body_GoToPoint) action; however, the agent will also change the neck direction to the ball.

### Bhv_NeckBodyToBall
This action gets one parameter:
- ```angel_buf``` (float): The buffer of the angle that the agent should turn its neck to the ball.

This action is as same as the [```Bhv_BodyNeckToBall```](#Bhv_BodyNeckToBall) action; however, the agent will not turn if the it can look at around the ball with the ```angel_buf``` angle.

### Bhv_NeckBodyToPoint
This action gets two parameter:
- ```point``` (```Vector2D```): The target point that the agent wants to move to.
- ```angel_buf``` (float): The buffer of the angle that the agent should turn its neck to the target point.

This action is as same as the [```Bhv_BodyNeckToPoint```](#Bhv_BodyNeckToPoint) action; however, the agent will not turn if the it can look at around the target point with the ```angel_buf``` angle.

### Bhv_ScanField
This action gets no parameter. This action is used to scan the field by turning around itself. This action is mostly used when the agent's position is not valid or the agent has no idea where the ball is.

### Body_AdvanceBall
This action gets no parameter. This action is used to kick and move the ball to the forward direction (toward opponent's goal).

### Body_ClearBall
This action gets no parameter. This action is used to clear the ball  to escapre from dangerous situation.

### Body_Dribble
This action gets 5 parameters:
- ```target_point``` (```Vector2D```): The target point that the agent wants to move to with the ball.
- ```distance_threshold``` (float): The distance threshold that the agent should reach to the target point.
- ```dash_power``` (float): The maximum dash power that the agent can use to move to the target point.
- ```dash_count``` (int): The number of the dash that the agent should use after kicking the ball.
- ```dodge``` (bool): Indicates whether the agent should avoid the opponents.

### Body_GoToPointDodge
This action gets 2 parameters:
- ```target_point``` (```Vector2D```): The target point that the agent wants to move to.
- ```dash_power``` (float): The maximum dash power that the agent can use to move to the target point.

This action is as same as the [```Body_GoToPoint```](#Body_GoToPoint) action; however, the agent will also avoid all players and the ball.

### Body_HoldBall
This action gets 3 parameters:
- ```do_turn``` (bool): Indicates whether the agent can turn around itself. (defalue value is ```false```)
- ```turn_to_target_point``` (```Vector2D```): The target point that the agent should to turn to. (default value is ```(0, 0)```)
- ```kick_target_point``` (```Vector2D```): The target point that the agent should kick the ball to. (default value is ```Vector2D.INVALIDATED```)

This action is used to hold the ball and avoid the opponents. The agent will turn to the target point and kick the ball to the target point.

### Body_Intercept
This action gets 2 parameters:
- ```save_recovery``` (bool): Indicates whether the agent should save the recovery. (default value is ```true```)
- ```face_point``` (```Vector2D```): The target point that the agent should face (neck angle) to. (default value is ```Vector2D.INVALIDATED```)

This action is used to intercept the ball. This action uses the [```intercept_table```](#InterceptTable) of the agent to find the fastest way to intercept the ball.

### Body_KickOneStep
This action gets 3 parameters:
- ```target_point``` (```Vector2D```): The target point that the agent wants to kick the ball to.
- ```first_speed``` (float): The first speed that the agent wants to kick the ball with.
- ```force_mode``` (bool): Indicates whether the agent should use the force mode. (default value is ```false```)

This action is used to kick the ball to the target point with the ```first_speed```. The agent will kick the ball with the maximum speed that the agent can kick the ball if the ```force_mode``` is enabled and the ball cannot reach the ```first_speed``` in the current situation.

### Body_StopBall
This action gets no parameter. This action is used to stop the ball.

### Body_StopDash
This action gets one parameter:
- ```save_recovery``` (bool): Indicates whether the agent should save the recovery.

This action is used to stop the agent from moving.

### Body_TackleToPoint
(TODO CHECK)

### Body_TurnToAngle
This action gets one parameter:
- ```angle``` (float): The angle that the agent should turn to. Note that the angle is global, not relative to the agent's body.

This action is used to turn the agent to the angle.

### Body_TurnToBall
This action gets one parameter:
- ```cycle``` (int): The number of cycles that the agent should turn to the ball.

This action is used to turn the agent to the ball.

### Body_TurnToPoint
This action gets two parameter:
- ```point``` (```Vector2D```): The target point that the agent wants to turn to.
- ```cycle``` (int): The number of cycles that the agent should turn to the target point.

This action is used to turn the agent to the target point.

### Focus_MoveToPoint
This action gets one parameters:
- ```target_point``` (```Vector2D```): The point that the agent should focus.

This action is used to focus on the target point. If the ```target_point``` is not in the vision area, this action finds the closest point in the vision area to focus. Also, the ```target_point``` should not be farther than the ```ServerParam.focus_area_lenght``` (TODO CHECK) from the agent.

### Focus_Reset
This action gets no parameter. This action is used to set the focus point on the agent itself.

### Neck_ScanField
This action gets no parameter. This action is used to scan the field evenly by turning the neck.

### Neck_ScanPlayers
This action gets no parameter. This action is used to scan the players by turning the neck.

### Neck_TurnToBallAndPlayer
This actino gets 3 parameters:
- ```side``` (Side): The side of the player that the agent should turn its neck to.
- ```uniform_number``` (int): The uniform number of the player that the agent should turn its neck to.
- ```count_threshold``` (int): If player's posCount is smaller than this value, agent simply turns neck to the ball.

This action is used to turn the agent's neck to the player. If the target player's ```pos_count``` was smaller than the ```count_threshold``` or the player was ```ghost```, the agent will turn its neck to the ball.

### Neck_TurnToBallOrScan
This action gets one parameter:
- ```count_threshold``` (int): If ball's posCount is smaller than this value, agent simply turns neck to the ball. otherwise it scans the field.

### Neck_TurnToBall
This action gets no parameter. This action is used to turn the agent's neck to the ball.

### Neck_TurnToGoalieOrScan
This action gets one parameter:
- ```count_threshold``` (int): If goalie's posCount is smaller than this value, agent simply turns neck to the goalie. otherwise it scans the field.

### Neck_TurnToLowConfTeammate
This action gets no parameter. This action is used to turn the agent's neck to the teammate that has the lowest confidence or highest ```pos_count```.

### Neck_TurnToPlayerOrScan
this actino gets 3 parameters:
- ```side``` (Side): The side of the player that the agent should turn its neck to.
- ```uniform_number``` (int): The uniform number of the player that the agent should turn its neck to.
- ```count_threshold``` (int): If player's posCount is smaller than this value, agent scans the field.

### Neck_TurnToPoint
This action gets one parameter:
- ```target_point``` (```Vector2D```): The target point that the agent should turn its neck to.

### Neck_TurnToRelative
This action gets one parameter:
- ```angle``` (float): The angle that the agent should turn its neck to. The angle is relative to the agent's body.

### View_ChangeWidth
This action gets one parameter:
- ```width``` (ViewWidth): The width of the agent's view. The value can be ```NARROW```, ```NORMAL```, or ```WIDE```.

### View_Normal
This action gets no parameter. This action is used to set the agent's view width to the ```NORMAL``` width.

### View_Synch
(TODO CHECK)

### View_Wide
This action gets no parameter. This action is used to set the agent's view width to the ```WIDE``` width.



## Action
The action contains only one action; however, this action can be one of the following actions:

- ```Dash```
- ```Turn```
- ```Kick```
- ```Tackle```
- ```Catch```
- ```Move```
- ```TurnNeck```
- ```ChangeView```
- ```Say```
- ```PointTo```
- ```PointToOf```
- ```AttentionTo```
- ```AttentionToOf```
- ```Log```
- ```DebugClient```
- ```Body_GoToPoint```
- ```Body_SmartKick```
- ```Bhv_BeforeKickOff```
- ```Bhv_BodyNeckToBall```
- ```Bhv_BodyNeckToPoint```
- ```Bhv_Emergency```
- ```Bhv_GoToPointLookBall```
- ```Bhv_NeckBodyToBall```
- ```Bhv_NeckBodyToPoint```
- ```Bhv_ScanField```
- ```Body_AdvanceBall```
- ```Body_ClearBall```
- ```Body_Dribble```
- ```Body_GoToPointDodge```
- ```Body_HoldBall```
- ```Body_Intercept```
- ```Body_KickOneStep```
- ```Body_StopBall```
- ```Body_StopDash```
- ```Body_TackleToPoint```
- ```Body_TurnToAngle```
- ```Body_TurnToBall```
- ```Body_TurnToPoint```
- ```Focus_MoveToPoint```
- ```Focus_Reset```
- ```Neck_ScanField```
- ```Neck_ScanPlayers```
- ```Neck_TurnToBallAndPlayer```
- ```Neck_TurnToBallOrScan```
- ```Neck_TurnToBall```
- ```Neck_TurnToGoalieOrScan```
- ```Neck_TurnToLowConfTeammate```
- ```Neck_TurnToPlayerOrScan```
- ```Neck_TurnToPoint```
- ```Neck_TurnToRelative```
- ```View_ChangeWidth```
- ```View_Normal```
- ```View_Synch```
- ```View_Wide```
- ```HeliosGoalie```
- ```HeliosGoalieMove```
- ```HeliosGoalieKick```
- ```HeliosShoot```
- ```HeliosChainAction```
- ```HeliosBasicOffensive```
- ```HeliosBasicMove```
- ```HeliosSetPlay```
- ```HeliosPenalty```
- ```HeliosCommunicaion```
