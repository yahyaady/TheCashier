# The Cashier Apps

The Cashier merupakan aplikasi kasir sederhana yang berfungsi untuk melakukan perhitungan transaksi barang/jasa dengan cara menginputkan jumlah, nama item, harga, dan memilih tipenya.

## Fungsionalitas
- User dapat memasukkan Nama Item, Jumlah Item, dan Harga
- User dapat memilih Tipe Barang/Jasa
- Pada bagian jumlah dan harga User harus mengisikan berupa angka (Tidak boleh karakter maupun huruf)
- Total Harga terdapat dipaling bawah

### Cara Kerja
- Dari Method `MainWindow` pada class `MainWindow.xaml.cs` kita mendeklarasikan 
``` csharp
        private Calculator calculator;
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }
```

- Inisialisasi List dan Perhitungaan Barang dan Jasa terdapat pada class `Item.cs` :
``` csharp
class Item
    {
        private int id;
        public string title { get; set; }
        public int quantity { get; set; }
        public double price { get; set; }
        public double subtotal { get; set; }
        private string type;

        public Item(int id, string title, int quantity, string type, double price)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.type = type;
            this.price = price;
            this.subtotal = 0;
        }
        public string getTitle()
        {
            return title;
        }
        public int getQuantity()
        {
            return quantity;
        }
        public string getType()
        {
            return type;
        }
        public double getPrice()
        {
            return price;
        }
        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
    }
```

- Perhitungan Total Suluruh Barang/Jasa yg telah diinput berada di Class `Calculator.cs` :
``` csharp
public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
```

- Menampilkan yang telah diinput pada ListBox terdapat di `MainWindow.xaml.cs`
``` csharp
private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, type, price);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp {0}", total);

            listBox.Items.Refresh();
        }
```
