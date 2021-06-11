## <p align="center"> Làm Game Rắn Săn Mồi Bằng Java </p>
<p align="center"> <img src="https://github.com/zukahai/HaiZuka/blob/master/Images/SnakeGame/1.png" alt="Tieude" /> </p>

### Làm Trò Chơi Rắn Săn Mồi Bằng Java
Chắn hẳn trong chúng ta cũng đã từng chơi trò rắn săn mồi trên chiếc điện thoại đen trắng. Cách chơi của game này rất dễ dàng chỉ cần điều khiển chú rắn làm sao để cho đầu của nó không đâm được vào thân và còn phải ăn những quả bóng điểm để chú rắn lớn hơn.

<p align="center"> <img src="https://github.com/zukahai/HaiZuka/blob/master/Images/SnakeGame/2.png" alt="Snake" /> </p>

### Dữ liệu cần thiết

#### 1. Phân biệt thân rắn, đầu rắn, thức ăn, khoảng trống

Để phần biệt thân rắn, đầu rắn, thức ăn, khoảng trống ta sử dụng một ma trận a.
```Java
	private int a[][] = new int[maxXY][maxXY];
```
Trong đó a[i][j] biểu diễn ô vuông (i, j) thông qua giá trị của nó:

- a[i][j] = 0: Là khoảng trống.
- a[i][j] = 1: Là thân rắn.
- a[i][j] = 2: Là đầu rắn.
- a[i][j] = 3: Là thức ăn.

####2. Thuộc tính của rắn trong trò chơi

Để có thể biểu diễn được con rắn trong game ta cần lưu đồ dài của con rắn (dùng biến sizeSnake) và các tọa độ các ô của thân rắn.
```Java
	private int xSnake[] = new int[maxXY * maxXY];
	private int ySnake[] = new int[maxXY * maxXY];
 ```
 Mỗi cặp tọa độ (xSnake[i], ySnake[i]) là một tọa đọ của thân răn, đặc biệt (xSnake[sizeSnake - 1], ySnake[sizeSnake - 1]) chính là tọa độ của đầu rắn.

Bên cạnh những thuộc tính trên ta cần lưu hướng di chuyển của con rắn bằng các sử dụng biến direction:

- direction =  1 có nghĩa là con rắn đang di chuyển lên trên của màn hình.
- direction =  2 có nghĩa là con rắn đang di chuyển sang phải của màn hình.
- direction =  3 có nghĩa là con rắn đang di chuyển xuống dưới của màn hình.
- direction =  4 có nghĩa là con rắn đang di chuyển sang trái của màn hình.
 
### Thiết lập giao diện

#### 1. Thiết lập giao diện

Phần giao diện của bài này ta sử dụng các button trong class JFrame của Pakage javax.swing

Ta sẽ tạo một ma trận JButton (kích thước m * n) để tạo giao diện cho trò chơi này.
```Java
  	public Container init(int k) {
		Container cn = this.getContentPane();
		pn = new JPanel();
		pn.setLayout(new GridLayout(m,n));
		for (int i = 0; i < m; i++)
			for (int j = 0; j < n; j++){
				bt[i][j] = new JButton();
				pn.add(bt[i][j]);
				bt[i][j].setActionCommand(i + " " + j);
				bt[i][j].addActionListener(this);
				bt[i][j].addKeyListener(this);
				bt[i][j].setBorder(null);
				a[i][j] = 0;
			}
		
		pn2 = new JPanel();
		pn2.setLayout(new FlowLayout());
		
		newGame_bt = new JButton("New Game");
		newGame_bt.addActionListener(this);
		newGame_bt.addKeyListener(this);
		newGame_bt.setFont(new Font("UTM Micra", 1, 15));
		newGame_bt.setBackground(Color.white);
		
		score_bt = new JButton("3");
		score_bt.addActionListener(this);
		score_bt.addKeyListener(this);
		score_bt.setFont(new Font("UTM Micra", 1, 15));
		score_bt.setBackground(Color.white);
		
		for (int i = 1; i <= speed.length; i++)
			lv.addItem("Mức độ " + i);
		lv.setSelectedIndex(k);
		lv.addKeyListener(this);
		lv.setFont(new Font("UTM Micra", 1, 15));
		lv.setBackground(Color.white);
		
		pn2.add(newGame_bt);
		pn2.add(lv);
		pn2.add(score_bt);
		
		a[m / 2][n / 2 - 1] = 1;
		a[m / 2][n / 2] = 1;
		a[m / 2][n / 2 + 1] = 2;
		xSnake[0] = m / 2;
		ySnake[0] = n / 2 - 1;
		xSnake[1] = m / 2;
		ySnake[1] = n / 2;
		xSnake[2] = m / 2;
		ySnake[2] = n / 2 + 1;
		sizeSnake = 3;
		
		creatFood();
		updateColor();
		cn.add(pn);
		cn.add(pn2, "South");
		this.setVisible(true);
		this.setSize(n * 30, m * 30);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		this.setLocationRelativeTo(null);
		return cn;
	}
```


## <p align="center">  :tv: Thanks for whatching :earth_africa: </p>
