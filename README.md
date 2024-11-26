# Activity-8
using System;
using System.Data.SqlClient;
using System.Configuration; 

namespace YourNamespace
{
    public partial class frmCustomerDataEntry : Form
    {
        public frmCustomerDataEntry()
        {
            InitializeComponent();
        }

        private void frmCustomerDataEntry_Load(object sender, EventArgs e)
        {
            loadCustomer();
        }

        private void loadCustomer()
        {
            string strConnection = ConfigurationManager.ConnectionStrings["DBConn"].ToString();
            
            using (SqlConnection objConnection = new SqlConnection(strConnection))
            {
                try
                {
                    objConnection.Open();
                    string strCommand = "SELECT * FROM CustomerTable";
                    using (SqlCommand objCommand = new SqlCommand(strCommand, objConnection))
                    {
                        DataSet objDataSet = new DataSet();
                        SqlDataAdapter objAdapter = new SqlDataAdapter(objCommand);
                        objAdapter.Fill(objDataSet);
                        dtgCustomer.DataSource = objDataSet.Tables[0];
                    }
                }
                catch (Exception ex)
                {
                    MessageBox.Show($"Error: {ex.Message}");
                }
            }
        }
    }
}
