<Pre>
    # gym_
Imports System.Data.OleDb
Imports System.Data
Partial Class MasterPage
    Inherits System.Web.UI.MasterPage
    Dim con As New OleDbConnection("Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\HP\Documents\Database3.mdb")
    Dim cmd As OleDbCommand
    Dim da As OleDbDataAdapter
    Dim ds As DataSet
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        con.Open()
        display()
    End Sub
    Sub display()
        da = New OleDbDataAdapter("select * from Table1", con)
        ds = New DataSet
        da.Fill(ds, "Table1")
        GridView1.DataSource = ds.Tables("Table1")
        GridView1.DataBind()
    End Sub
    Sub clear()
        TextBox1.Text = ""
        TextBox2.Text = ""
        TextBox3.Text = ""
     End Sub

    Protected Sub GridView1_SelectedIndexChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles GridView1.SelectedIndexChanged
        display()
    End Sub

    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
        cmd = New OleDbCommand("insert into Table1(name,lastname)values(@name,@lastname)", con)
        cmd.Parameters.AddWithValue("@name", TextBox2.Text)
        cmd.Parameters.AddWithValue("@lastname", TextBox3.Text)
        cmd.ExecuteNonQuery()
        display()
        clear()
    End Sub

    Protected Sub Button2_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button2.Click
        cmd = New OleDbCommand("select * from Table1 where id=@id", con)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)
        Dim render As OleDbDataReader = cmd.ExecuteReader()
        render.Read()
        TextBox2.Text = render("name").ToString()
        TextBox3.Text = render("lastname").ToString()
        render.Close()
        con.Close()

    End Sub

    Protected Sub Button3_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button3.Click
        cmd = New OleDbCommand("update Table1 set name=@name, lastname=@lastname where id=@id", con)
        cmd.Parameters.AddWithValue("@name", TextBox2.Text)
        cmd.Parameters.AddWithValue("@lastname", TextBox3.Text)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)
        cmd.ExecuteNonQuery()
        display()
        clear()
    End Sub

    Protected Sub Button5_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button5.Click
        clear()
    End Sub

    Protected Sub Button4_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button4.Click
        cmd = New OleDbCommand("delete from Table1 where id=@id", con)
        cmd.Parameters.AddWithValue("@id", TextBox1.Text)
        cmd.ExecuteNonQuery()
        display()
        clear()
    End Sub
End Class


</Pre>
