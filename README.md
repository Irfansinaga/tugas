/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package tugas.besar;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;

 
public class Koneksaya {
    Connection conn = null;
    
    public Koneksaya(){
        try{
            Class.forName("com.mysql.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/inputnilai", "root", "");
        }
        catch(ClassNotFoundException ex){
            ex.printStackTrace();
        }
        catch(SQLException ex){
            ex.printStackTrace();
        }
}
    public void insertnilai(ListField m){
        if(m != null){
            try {
                PreparedStatement p = conn.prepareStatement("insert into inputnilai "
                        + "(nrp, nama, tingkat  "
                        + "programstudi,konsentrasi, tugas, kuis,uts,uas) values (?, ?, ?, ?, ?, ?, ?,?,?)");
                p.setString(1, m.getnrp());
                p.setString(2, m.getnama());
                p.setString(3, m.gettingkat());
                p.setString(4, m.getprogramstudi());
                p.setString(5, m.getkonsentrasi());
                p.setString(6, m.gettugas());
                p.setString(7, m.getkuis());
                p.setString(8, m.getuts());
                p.setString(9, m.getuas());
                p.executeUpdate();
                
            } catch (SQLException ex) {
            }
        }
    }
    
    public void updateMahasiswa(ListField m){
        if(m != null){
            try {
                PreparedStatement p = conn.prepareStatement("update inputnilai "
                        + "set nama = ?,  " +
                        " jurusan = ?, "
                        + "programstudi = ?,konsentrasi = ?, tugas = ?, " +
                        "kuis = ?, tugas= ?, uts= ? , uas= ?  where nrp = ? ");
                p.setString(1, m.getnrp());
                p.setString(2, m.getnama());
                p.setString(3, m.gettingkat());
                p.setString(4, m.getprogramstudi());
                p.setString(5, m.getkonsentrasi());
                p.setString(6, m.gettugas());
                p.setString(7, m.getkuis());
                p.setString(6, m.getuts());
                p.setString(7, m.getuas());
                p.executeUpdate();
            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }
    
    public void deleteMahasiswa(ListField m){
        if(m != null){
            try {
                PreparedStatement p = conn.prepareStatement("delete from inputnilai "
                        + "where nrp = ? ");
                p.setString(1, m.getnrp());
                p.executeUpdate();

            } catch (SQLException ex) {
                ex.printStackTrace();
            }
        }
    }
    
    public ArrayList<ListField> caridata(){
        ArrayList<ListField> lsMahasiswa = new ArrayList<ListField>();
        try {
            Statement statement = conn.createStatement();
            ResultSet rs = statement.executeQuery("select * from inputnilai");
            while(rs.next()){
                ListField m = new ListField();
                m.setnrp(rs.getString(1));
                m.setnama(rs.getString(2));
                m.settingkat(rs.getString(3));
                m.setprogramstudi(rs.getString(4));
                m.setkonsentrasi(rs.getString(5));
                m.settugas(rs.getString(6));
                m.setkuis(rs.getString(7));
                m.setuts(rs.getString(8));
                m.setuas(rs.getString(9));
                lsMahasiswa.add(m);
            }
        } catch (SQLException ex) { 
        }
        return lsMahasiswa;
    }
 
    
    public boolean isDuplicate(String nrp){
        boolean duplicate = false;

        try {
            Statement statement = conn.createStatement();
            ResultSet rs = statement.executeQuery("select * from inputnilai " +
                    "where nrp = '" + nrp + "'");
            duplicate = rs.next();
        } catch (SQLException ex) {
        }
        return duplicate;
    }
    
    
}
