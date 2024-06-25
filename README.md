Form 1

using System;
using System.ComponentModel;
using System.Drawing;
using System.Globalization;
using System.IO;
using System.Threading;
using System.Windows.Forms;

namespace Piksajkin.Sasha
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            this.Size = new Size(1060, 500);
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string[] ss = System.IO.Directory.GetDirectories("ggg");
            foreach (string s in ss)
                comboBox1.Items.Add(s.Remove(0,4));
        }

        private void Form1_FormClosed(object sender, FormClosedEventArgs e)
        {
            this.Hide();
            Form2 f2 = new Form2();
            f2.Show();
        }
            private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
            {
                richTextBox1.LoadFile("ggg/" + comboBox1.SelectedItem + "/info.rtf");
                listBox1.Items.Clear();
                button1.Visible = false;
                pictureBox1.Visible = false;
                richTextBox1.Visible = true;
                string[] ss = System.IO.Directory.GetFiles("ggg/" + comboBox1.SelectedItem + "/", "*.jpg");
                foreach (string s in ss)
                {
                    FileInfo f = new FileInfo(s);
                    listBox1.Items.Add(f.Name);
                }
            }

            private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
            {
                if (listBox1.SelectedIndex == -1)
                {

                }
                else
                {
                    pictureBox1.Image = Image.FromFile(@"ggg/" + comboBox1.Text + "/" + listBox1.SelectedItem.ToString());
                }
                
                richTextBox1.Visible = false;
                pictureBox1.Visible = true;
                button1.Visible = true;
            }

            private void button1_Click(object sender, EventArgs e)
            {
                richTextBox1.Visible = true;
                button1.Visible = false;
            }
    }
}
Form 2

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Globalization;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Piksajkin.Sasha
{
    public partial class Form2 : Form
    {
        
        public Form2()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            this.Hide();
            Form1 f1 = new Form1();
            f1.Show(); 
        }

        private void button3_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        private void Form2_Load(object sender, EventArgs e)
        {

        }
    }
}
Program

using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Piksajkin.Sasha
{
    static class Program
    {
        /// <summary>
        /// Главная точка входа для приложения.
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new Form2());
        }
    }
}
