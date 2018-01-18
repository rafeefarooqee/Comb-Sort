# Comb-Sort
  using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;  

namespace CombSort
{
    class Sort
    {
        private double Gap(double gap)
        {
            return gap / 1.3;
        }
        private void Swap(ref byte a, ref byte b)
        {
            byte c = a;
            a =b;
            b = c;
        }
        public void CombSort(ref byte[] arr)
        {
            double gap = arr.Length;
            bool swap = true;

            while(gap!=1 || swap==true)
            {
                gap = Gap(gap);
                swap = false;

                if (gap < 1)
                {
                    gap = 1;
                }
                int igap = (int)gap;
                
                
                for(int i=0; i< arr.Length - igap; i++)
                {
                    if (arr[i] > arr[i + igap])
                    {
                        Swap(ref arr[i], ref arr[i + igap]);
                        swap = true;
                    }
                    
                }

            }
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Sort s = new Sort();
            string myFile = @"C:\Users\Rafi\Documents\Visual Studio 2015\Projects\CombSort\data.txt";
            byte[] a = new byte[9] { 8, 4, 1, 56, 3, 44, 6, 28, 0 };
            byte[] b = new byte[9];
            using (BinaryWriter w = new BinaryWriter(File.Open(myFile, FileMode.Create)))
            {
                w.Write(a, 0, a.Length);
            }
            if (File.Exists(myFile))
            {
                using (BinaryReader r = new BinaryReader(File.Open(myFile, FileMode.Open)))
                {
                    r.Read(b, 0, b.Length);
                }
                
            }

            s.CombSort(ref b);
            
            for(int i=0; i<b.Length; i++)
            {
                Console.WriteLine(b[i]);
            }
            Console.ReadLine();
        }
    }
}
