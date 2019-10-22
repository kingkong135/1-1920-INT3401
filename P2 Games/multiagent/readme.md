Đây là "[***Project 2: Multi-Agent Search***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/)". Gồm 5 câu hỏi:
* "[***Question 1 (4 points): Reflex Agent***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/#question-1-4-points-reflex-agent)" 

   Viết hàm đánh giá evaluationFunction trả về số điểm nếu pacman đi vào vị trí đó, ở trong câu hỏi này là bản đồ đơn giản.
   
   Cách làm:
   - Tìm khoảng cách gần nhât giữa pacman đến con ma gần nhất và khoảng cách gẫn nhất từ pacman đến thưc ăn gần nhất. Khởi tạo cả 2 là vô cùng (1000).
   - Hàm trả về giá trị successorGameState.getScore() - 20 / (nearestGhostDistance + 1) + 5 / (nearestFoodDistance + 1)
   
  "[***Code câu hỏi thứ 1 tại đây***](https://github.com/kingkong135/1-1920-INT3401/blob/2d976fac77a7762e7195bbd11085956b0da82a30/P2%20Games/multiagent/multiAgents.py#L79)" 
   
* "[***Question 2 (5 points): Minimax***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/#question-2-5-points-minimax)" 

   Triển khai thuật toán Minimax.
   
   Cách làm:
   - Khơi tạo biến global bestAction là hoạt động tốt nhất
   - Sẽ dùng đệ quy viết hàm minimax(player, depth, isPac, state). Với player là số thứ tự player, 0 là pacman, 1,2 là ma; depth là độ sâu của cây tìm kiếm, isPac xem có phải là pacman không, state là trạng thái hiện tại
   - Trạng thái kết thúc nếu depth = 0 hoặc state.isWin() hoặc    state.isLose()
   - Nếu là Pacman: khởi tạo score = -10000, xét các hoạt động tiếp theo của pacman. Với mỗi hoạt động thì ta sẽ gọi v = minimax(nextPlayer, depth, False, newState) là số điểm của con ma tiếp theo, sẽ có cùng độ sâu. trả lai action nếu v > score và depth = self.depth. Cập nhật lai score = max(v, score). Vì Pacman sẽ tìm max khoảng cách giữa nó và các con ma.
   - Nếu là ma: thì sẽ làm ngược lại. Khởi tọa score = -10000, xác định các trạng thai tiếp theo của playeer tiếp theo. sẽ cập nhật lại độ sâu nếu người chơi tiếp theo là pacman nếu không thì giữ nguyên độ sâu. Gọi đệ quy v = minimax(nextPlayer, tempPly, isPac, newState). và cập nhật lại score = min(score, v). Vì các con ma sẽ min khoảng cách giữa nó và các con ma.
   - Băt đầu chạy minimax(0, self.depth, True, gameState)
   
  "[***Code câu hỏi thứ 2 tại đây***](https://github.com/kingkong135/1-1920-INT3401/blob/2d976fac77a7762e7195bbd11085956b0da82a30/P2%20Games/multiagent/multiAgents.py#L155)"
   
 * "[***Question 3 (5 points): Alpha-Beta Pruning***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/#question-3-5-points-alpha-beta-pruning)" 

   Triển khai thuật toán Alplha-Beta pruning để tỉa cây tìm kiếm ở thuật toán Minimax với alpha là giá trị max tốt nhất và beta là giá trị min tốt nhất.
   
   Cách làm:
   - Tương tự như câu hỏi thứ 2 nhưng sẽ thêm tham số anlpha và beta
   - Các thực hiện dựa trên mã giả trong bài giảng "[***Link***](https://inst.eecs.berkeley.edu/~cs188/su19/assets/images/alpha_beta_impl.png)"
  
  "[***Code câu hỏi thứ 3 tại đây***](https://github.com/kingkong135/1-1920-INT3401/blob/2d976fac77a7762e7195bbd11085956b0da82a30/P2%20Games/multiagent/multiAgents.py#L188)"
   
* "[***Question 4 (5 points): Expectimax***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/#question-4-5-points-expectimax)" 

   Minimax và alpha-beta là tuyệt vời, nhưng cả hai đều cho rằng bạn đang chơi với một kẻ thù đưa ra quyết định tối ưu. Như bất cứ ai đã từng giành được tic-tac-toe đều có thể nói với bạn, điều này không phải lúc nào cũng đúng. Trong câu hỏi này, bạn sẽ thực hiện **ExpectimaxAgent**, rất hữu ích cho việc mô hình hóa hành vi xác suất của các tác nhân có thể đưa ra lựa chọn dưới mức tối ưu. Hay còn gọi là thuật toán tối ưu mong đợi
   
   Cách làm:
   - Tương tự như thuật toan thứ 2 nhưng thay vì tim min khi người chơi là ma, thì sẽ tính trung bình score các hành động 
   
  "[***Code câu hỏi thứ 4 tại đây***](https://github.com/kingkong135/1-1920-INT3401/blob/2d976fac77a7762e7195bbd11085956b0da82a30/P2%20Games/multiagent/multiAgents.py#L239)"
   
* "[***Question 5 (6 points): Evaluation Function***](https://inst.eecs.berkeley.edu/~cs188/su19/project2/#question-5-6-points-evaluation-function)" 

   Viết hàm đánh giá evaluationFunction trả về số điểm nếu pacman đi vào vị trí đó. Nhưng ở đây sẽ khó hơn vì bản đồ có nhiều chướng ngại vật
   
   Cách làm:
   - Ta sẽ xét nhiều yếu tố như : số thức ăn còn lại, số viên năng (viên trắng to), số lượng ma còn lại, khoảng cách giữa pacman và thức găn gần nhất, khoảng cách giữa pacman và ma gần nhất.
   
  "[***Code câu hỏi thứ 5 tại đây***](https://github.com/kingkong135/1-1920-INT3401/blob/2d976fac77a7762e7195bbd11085956b0da82a30/P2%20Games/multiagent/multiAgents.py#L288)"
   
   
