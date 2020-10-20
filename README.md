# TheCashier
	Sebuah aplikasi kasir yang juga sebagai tugas kuliah saya dalam matakuliah Pemograman Lanjut.

# Fungsionalitas
  Sebuah aplikasi untuk kemudahan seorang kasir dalam menghitung barang/jasa belanjaan pembeli, dengan penginputan nama barang/jasa, jumlah, serta 
  harga yang dapat ditambahkan dalam sebuah listbox dengan sudah terjumlahkan secara otomatis. Total harga tersedia pada sudut bawah kiri jendela.
  
# Class item

Setelah pendeklarasian pada class item, dilanjutkan dengan penginisialisasian seluruh bahan sebagai media yang nantinya akan menjadi perwakilan dari
variable yang akan diinputkan oleh pengguna.
    
    public Item(int id, string title, int quantity, string type, double price)
		{
			this.id = id;
			this.title = title;
			this.quantity = quantity;
			this.type = type;
			this.price = price;
			this.subtotal = 0;
		}

Selanjutnya semua bahan akan di buatkan semacam variable perwakilan untuk input. Dibawah ini, terjadi proses dimana nilai dari subtotal diambil dari 
perkalian nilai price dengan quantity yang selanjutnya akan mewakili getSubtotal() 

		public double getSubTotal()
		{
			subtotal = price * quantity;
			return subtotal;
		}

# Class Calculator

Dibawah ini berfungsi sebagai penginisialisasian data dari input akan dimasukan dalam satu list yaitu listItem, serta penambahan nilai dari total jika 
item baru diinputkan ke dalam list secara otomatis

        private List<Item> listItem;
        private double total = 0;

        public Calculator()
        {
            this.listItem = new List<Item>();
        }

Disini juga mewakilkan dari single responsibility dimana suatu proses hanya mempertanggungjawabkan satu aksi yaitu
pengambilan inputan untuk ditampilkan dalam list.
        public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }

Lalu berpindah ke MainWindow.xaml.cs sebagai pusat dari semua proses. Dimulai dari pengambilan seluruh bahan-bahan yang digunakan, seperti listItem
  
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }

Dan puncak proses dari aplikasi TheCashier ini ada pada koding berikut.

private void AddButton_Click(object sender, RoutedEventArgs e)
        {

            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);


            Item item = new Item(new Random().Next(), title, quantity, type, price);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = String.Format("Rp. {0}", total);

            listBox.Items.Refresh();
        }

Dimana setelah semua input sudah terbaca, lalu diproses dan di output kan dengan cara ditampilkan dalam listItem dan label yang berada pada sudut 
bawah. Label tersebut menunjukan total dari seluruh item yang di input kan berserta total harga dan keterangan lainnya.
  
