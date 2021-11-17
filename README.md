# EslestirmeOyunu
Windows Form İle Hafıza Oyunu Yapımı.

*
*
*

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace EslestirmeOyunu
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
            iconatama();
            t.Tick += T_Tick;
            t.Start();
            t.Interval = 3000;
            t1.Tick += T1_Tick;
        }

        private void T1_Tick(object sender, EventArgs e)
        {
            t1.Stop();
            first.ForeColor = first.BackColor;
            second.ForeColor = second.BackColor;
            first = null;
            second = null;

        }

        private void T_Tick(object sender, EventArgs e)
        {
            t.Stop();
            foreach (Button item in Controls)
            {
                item.ForeColor = item.BackColor;
            }
        }

        List<string> iconlar = new List<string>()
        {
            "a","b","c","d","e","f","g","h","i",",","!","N",
            "a","b","c","d","e","f","g","h","i",",","!","N"
        };
        Random rnd = new Random();
        int randomindex;
        Timer t = new Timer();
        Timer t1 = new Timer();
        Button first, second;
        Button butonlar;
        private void Form1_Load(object sender, EventArgs e)
        {
           
        }
        private void iconatama()
        {
            Button btn;
            foreach (Button item in Controls)
            {
                btn = item as Button;
                randomindex = rnd.Next(iconlar.Count);
                btn.Text = iconlar[randomindex];
                btn.ForeColor = Color.Black;
                iconlar.RemoveAt(randomindex);
            }
        }

        private void button_Click(object sender, EventArgs e)
        {
            Button btn = sender as Button;
            if (first == null)
            {
                first = btn;
                first.ForeColor = Color.Black;
                return;
            }
            second = btn;
            second.ForeColor = Color.Black;
            if (first.Text == second.Text)
            {
                first.ForeColor = Color.Black;
                second.ForeColor = Color.Black;
                first = null;
                second = null;
            }
            else
            { 
                t1.Start();
                t1.Interval = 2000;
            }
        }
    }
}
