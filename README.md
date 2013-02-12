
// Koneksi Ke Database 
 
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
  
//-------------------------------------------------------------------------------------------------

//Skrip ListField.java



package tugas.besar;


public class ListField {
    private String nrp;
    private String nama;
    private String tingkat;
    private String programstudi;
    private String konsentasi;
    private String tugas;
    private String kuis;
    private String uts;
    private String uas;
 
    public String getnrp() {
        return nrp;
    }

    
    public void setnrp(String nrp) {
        this.nrp = nrp;
    }

   
    public String getnama() {
        return nama;
    }

  
    public void setnama(String nama) {
        this.nama = nama;
    }

              
    public String gettingkat() {
        return tingkat;
    }

    
    
    public void settingkat(String tingkat) {
        this.tingkat = tingkat;
    }

   
       
     public String getprogramstudi() {
        return programstudi;
    }

    
    public void setprogramstudi(String programstudi) {
        this.programstudi = programstudi;
    }

    public String getkonsentrasi() {
        return konsentasi;
    }

    
    public void setkonsentrasi(String konsentrasi) {
        this.konsentasi = konsentrasi;
    }

    
    public String gettugas() {
        return tugas;
    }

   
    public void settugas(String tugas) {
        this.tugas = tugas;
    }

    
        
    public String getkuis() {
        return kuis;
    }

        
    public void setkuis(String kuis) {
        this.kuis =kuis;
    }

   
    public String getuts() {
        return uts;
    }

   
    public void setuts(String uts) {
        this.uts   = uts;
    }
    
    public String getuas() {
        return uas;
    }

   
    public void setuas(String uas) {
        this.uas   = uas;
    }
    
}


//--------------------------------------------------------------
//Skirp dari TugasBesar.java

/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package tugas.besar;

/**
 *
 * @author JesusDieForMe
 */
public class TugasBesar {

    public TugasBesar(){
        JForm app = new JForm();
        app.setVisible(true);
        app.setSize(500, 500);
       app.pack();
    } 
    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
     new TugasBesar();
     
    }
}


//----------------------------------------------------------------------------------
// Skrip dari Form (JForm.java)


package tugas.besar;

     import java.util.ArrayList;
     import java.util.Iterator;
     import javax.swing.DefaultListModel;
     import javax.swing.JOptionPane;
     import javax.swing.table.DefaultTableModel;
     import javax.swing.table.TableColumn;
     import javax.swing.ComboBoxModel;



public class JForm extends javax.swing.JFrame {
   
    private ArrayList<ListField> lsMahasiswa = new ArrayList<ListField>();
    private DefaultListModel dfm = new DefaultListModel();
    private Koneksaya myCon = null;
    private ListField selectedMahasiswa = null;
    private DefaultTableModel tbModel = null;
    
    
    
    public JForm() {
      
        myCon = new Koneksaya();
        initComponents();
       init();
       refreshnilai();
       refreshnilaiontable();
       refreshDetailNilai();
       cTingkat.addItem("1");
       cTingkat.addItem("2");
       cTingkat.addItem("3");
       cTingkat.addItem("4");
    }
private void refreshnilai(){
        dfm.removeAllElements();
        lsMahasiswa = myCon.caridata();

        for (Iterator<ListField> it = lsMahasiswa.iterator(); it.hasNext();) {
            ListField mahasiswa = it.next();
            dfm.addElement(mahasiswa.getnama());
        }
    }
    
 private void refreshnilaiontable(){
        if(tbModel.getRowCount() > 0){
            for (int i=0;i<=tbModel.getRowCount();i++){
                tbModel.removeRow(i);
            }
        }
            for (Iterator<ListField> it = lsMahasiswa.iterator(); it.hasNext();) {
                ListField mahasiswa = it.next();
                tbModel.addRow(new String[] {
                    mahasiswa.getnrp(),
                    mahasiswa.getnama(),
                    mahasiswa.gettingkat(),
                    mahasiswa.getprogramstudi(),
                    mahasiswa.getkonsentrasi(),
                    mahasiswa.gettugas(),
                    mahasiswa.getkuis(),
                    mahasiswa.getuts(),
                    mahasiswa.getuas()
                });
            }
    }

 private void refreshDetailNilai(){
        if(selectedMahasiswa != null){
            tnrp.setText(selectedMahasiswa.getnrp());
            tNama.setText(selectedMahasiswa.getnama());
            if(selectedMahasiswa.getprogramstudi().equals("Administrasi Niaga")){
                cProgramStudi.setSelectedIndex(1);
            }
            else if(selectedMahasiswa.getprogramstudi().equals("Akuntansi")){
                cProgramStudi.setSelectedIndex(2);
            }
            else if(selectedMahasiswa.getprogramstudi().equals("Manajemen Informatika")){
                cProgramStudi.setSelectedIndex(3);
            }

            if(selectedMahasiswa.getkonsentrasi().equals("Sekretaris")){
                cKonsentrasi.setSelectedIndex(0);
            }
            else if(selectedMahasiswa.getkonsentrasi().equals("Manajemen")){
                cKonsentrasi.setSelectedIndex(1);
            }
            else if(selectedMahasiswa.getkonsentrasi().equals("Komputer Akuntansi")){
                cKonsentrasi.setSelectedIndex(0);
            }
            else if(selectedMahasiswa.getkonsentrasi().equals("Perpajakan")){
                cKonsentrasi.setSelectedIndex(1);
            }
            else if(selectedMahasiswa.getkonsentrasi().equals("Teknik Informatika")){
                cKonsentrasi.setSelectedIndex(0);
            }
            else if(selectedMahasiswa.getkonsentrasi().equals("Manajemen Informatika")){
                cKonsentrasi.setSelectedIndex(1);
            }

        
            
    }
 }
 
 private void clean(){
      

        tnrp.setText("");
        tTugas.setText("");
        tUTS.setText("");
        tUAS.setText("");
        tnrp.setText("");
        tNama.setText("");
        cTingkat.removeAllItems();
        cKonsentrasi.removeAllItems();
        cProgramStudi.removeAllItems();
 }
    private void init(){
        jlMahasiswa.setModel(dfm);
        cProgramStudi.addItem("--Pilih Program Studi--");
        cProgramStudi.addItem("Administrasi Niaga");
        cProgramStudi.addItem("Akuntansi");
        cProgramStudi.addItem("Manajemen Informatika");
        

        tbModel = new DefaultTableModel();

        tbModel.addColumn("NRP");
        tbModel.addColumn("Nama");
        tbModel.addColumn("Tingkat");
        tbModel.addColumn("Program Studi");
        tbModel.addColumn("Konsentrasi");
        tbModel.addColumn("Tugas");
        tbModel.addColumn("Kuis");
        tbModel.addColumn("UTS");
        tbModel.addColumn("UAS");

        TbMahasiswa.setModel(tbModel);

        TableColumn tcnrp = TbMahasiswa.getColumnModel().getColumn(0);
        TableColumn tcNama = TbMahasiswa.getColumnModel().getColumn(1);
        TableColumn tctingkat = TbMahasiswa.getColumnModel().getColumn(2);
        TableColumn tcprogramstudi = TbMahasiswa.getColumnModel().getColumn(2);
        TableColumn tckonsentrasi = TbMahasiswa.getColumnModel().getColumn(3);
        TableColumn tctugas = TbMahasiswa.getColumnModel().getColumn(4);
        TableColumn tckuis = TbMahasiswa.getColumnModel().getColumn(5);
        TableColumn tcuts = TbMahasiswa.getColumnModel().getColumn(6);
        TableColumn tcuas = TbMahasiswa.getColumnModel().getColumn(7);

        tcnrp.setWidth(tcnrp.getWidth());
        tcNama.setWidth(tcNama.getMaxWidth());
        tctingkat.setWidth(tctingkat.getMaxWidth());
        tcprogramstudi.setWidth(tcprogramstudi.getMaxWidth());
        tckonsentrasi.setWidth(tckonsentrasi.getMaxWidth());
        tctugas.setWidth(tctugas.getMaxWidth());
        tckuis.setWidth(tckuis.getMaxWidth());
        tcuts.setWidth(tcuts.getMaxWidth());
        tcuas.setWidth(tcuas.getMaxWidth());
    }

    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jPanel2 = new javax.swing.JPanel();
        tNama = new javax.swing.JTextField();
        jLabel2 = new javax.swing.JLabel();
        jLabel3 = new javax.swing.JLabel();
        jPanel3 = new javax.swing.JPanel();
        jLabel4 = new javax.swing.JLabel();
        jSeparator2 = new javax.swing.JSeparator();
        jLabel5 = new javax.swing.JLabel();
        cProgramStudi = new javax.swing.JComboBox();
        jLabel6 = new javax.swing.JLabel();
        jLabel7 = new javax.swing.JLabel();
        cKonsentrasi = new javax.swing.JComboBox();
        cTingkat = new javax.swing.JComboBox();
        jSeparator3 = new javax.swing.JSeparator();
        jSeparator4 = new javax.swing.JSeparator();
        jLabel8 = new javax.swing.JLabel();
        jSeparator5 = new javax.swing.JSeparator();
        tKuis = new javax.swing.JTextField();
        jLabel10 = new javax.swing.JLabel();
        jLabel9 = new javax.swing.JLabel();
        tTugas = new javax.swing.JTextField();
        jLabel11 = new javax.swing.JLabel();
        jLabel12 = new javax.swing.JLabel();
        tUAS = new javax.swing.JTextField();
        tUTS = new javax.swing.JTextField();
        tnrp = new javax.swing.JTextField();
        jPanel1 = new javax.swing.JPanel();
        jLabel1 = new javax.swing.JLabel();
        jSeparator1 = new javax.swing.JSeparator();
        jPanel4 = new javax.swing.JPanel();
        jScrollPane2 = new javax.swing.JScrollPane();
        jlMahasiswa = new javax.swing.JList();
        jScrollPane1 = new javax.swing.JScrollPane();
        TbMahasiswa = new javax.swing.JTable();
        btSimpan = new javax.swing.JButton();
        btHapus = new javax.swing.JButton();

        addInputMethodListener(new java.awt.event.InputMethodListener() {
            public void caretPositionChanged(java.awt.event.InputMethodEvent evt) {
            }
            public void inputMethodTextChanged(java.awt.event.InputMethodEvent evt) {
                formInputMethodTextChanged(evt);
            }
        });

        tNama.setName("tNamaLengkap"); // NOI18N
        tNama.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                tNamaActionPerformed(evt);
            }
        });

        jLabel2.setText("NRP");

        jLabel3.setText("Nama");

        jLabel4.setFont(new java.awt.Font("Verdana", 1, 12));
        jLabel4.setText("Identitas Mahasiswa");

        javax.swing.GroupLayout jPanel3Layout = new javax.swing.GroupLayout(jPanel3);
        jPanel3.setLayout(jPanel3Layout);
        jPanel3Layout.setHorizontalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel3Layout.createSequentialGroup()
                .addGap(169, 169, 169)
                .addComponent(jSeparator2, javax.swing.GroupLayout.DEFAULT_SIZE, 1, Short.MAX_VALUE)
                .addContainerGap())
            .addGroup(jPanel3Layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jLabel4, javax.swing.GroupLayout.PREFERRED_SIZE, 155, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(5, 5, 5))
        );
        jPanel3Layout.setVerticalGroup(
            jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel3Layout.createSequentialGroup()
                .addGroup(jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel3Layout.createSequentialGroup()
                        .addGap(28, 28, 28)
                        .addComponent(jSeparator2, javax.swing.GroupLayout.PREFERRED_SIZE, 10, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addComponent(jLabel4))
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
        );

        jLabel5.setText("Tingkat");

        cProgramStudi.addItemListener(new java.awt.event.ItemListener() {
            public void itemStateChanged(java.awt.event.ItemEvent evt) {
                cProgramStudiItemStateChanged(evt);
            }
        });
        cProgramStudi.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                cProgramStudiActionPerformed(evt);
            }
        });

        jLabel6.setText("Program Studi:");

        jLabel7.setText("Konsentrasi:");

        cTingkat.setInheritsPopupMenu(true);
        cTingkat.addItemListener(new java.awt.event.ItemListener() {
            public void itemStateChanged(java.awt.event.ItemEvent evt) {
                cTingkatItemStateChanged(evt);
            }
        });
        cTingkat.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                cTingkatActionPerformed(evt);
            }
        });

        jLabel8.setFont(new java.awt.Font("Verdana", 1, 12));
        jLabel8.setText("Input Nilai");

        tKuis.setName("tNamaLengkap"); // NOI18N

        jLabel10.setText("Kuis");

        jLabel9.setText("Tugas");

        tTugas.setName("tNamaLengkap"); // NOI18N

        jLabel11.setText("UTS");

        jLabel12.setText("UAS");

        tUAS.setName("tNamaLengkap"); // NOI18N

        tUTS.setName("tNamaLengkap"); // NOI18N

        tnrp.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                tnrpActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
        jPanel2.setLayout(jPanel2Layout);
        jPanel2Layout.setHorizontalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jPanel3, javax.swing.GroupLayout.PREFERRED_SIZE, 168, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addContainerGap()
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel2)
                            .addComponent(jLabel3)
                            .addComponent(jLabel5)
                            .addComponent(jLabel6)
                            .addComponent(jLabel7))
                        .addGap(17, 17, 17)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(tnrp, javax.swing.GroupLayout.DEFAULT_SIZE, 121, Short.MAX_VALUE)
                            .addComponent(cProgramStudi, 0, 121, Short.MAX_VALUE)
                            .addComponent(cKonsentrasi, 0, 121, Short.MAX_VALUE)
                            .addComponent(cTingkat, javax.swing.GroupLayout.PREFERRED_SIZE, 58, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(tNama, javax.swing.GroupLayout.PREFERRED_SIZE, 121, javax.swing.GroupLayout.PREFERRED_SIZE))))
                .addGap(479, 479, 479))
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jLabel8, javax.swing.GroupLayout.PREFERRED_SIZE, 155, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap(533, Short.MAX_VALUE))
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING, false)
                    .addGroup(javax.swing.GroupLayout.Alignment.LEADING, jPanel2Layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jSeparator5))
                    .addComponent(jSeparator3, javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jSeparator4, javax.swing.GroupLayout.Alignment.LEADING, javax.swing.GroupLayout.DEFAULT_SIZE, 267, Short.MAX_VALUE))
                .addContainerGap())
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jLabel9)
                    .addComponent(jLabel10)
                    .addComponent(jLabel11)
                    .addComponent(jLabel12))
                .addGap(17, 17, 17)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                    .addComponent(tUTS, javax.swing.GroupLayout.Alignment.LEADING, javax.swing.GroupLayout.DEFAULT_SIZE, 70, Short.MAX_VALUE)
                    .addComponent(tKuis, javax.swing.GroupLayout.Alignment.LEADING, javax.swing.GroupLayout.DEFAULT_SIZE, 70, Short.MAX_VALUE)
                    .addComponent(tUAS, javax.swing.GroupLayout.DEFAULT_SIZE, 70, Short.MAX_VALUE)
                    .addComponent(tTugas, javax.swing.GroupLayout.Alignment.LEADING, javax.swing.GroupLayout.PREFERRED_SIZE, 70, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addGap(572, 572, 572))
        );
        jPanel2Layout.setVerticalGroup(
            jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel2Layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jPanel3, javax.swing.GroupLayout.PREFERRED_SIZE, 28, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addComponent(jSeparator4, javax.swing.GroupLayout.PREFERRED_SIZE, 10, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(1, 1, 1)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(jLabel2)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addComponent(jLabel3)
                        .addGap(18, 18, 18)
                        .addComponent(jLabel5))
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(tnrp, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(tNama, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                        .addComponent(cTingkat, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(cProgramStudi, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel6))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(cKonsentrasi, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jLabel7))
                .addGap(13, 13, 13)
                .addComponent(jSeparator3, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(3, 3, 3)
                .addComponent(jLabel8)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addComponent(jSeparator5, javax.swing.GroupLayout.PREFERRED_SIZE, 7, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(jLabel9)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addComponent(jLabel10))
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addComponent(tTugas, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(tKuis, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                        .addComponent(jLabel11)
                        .addComponent(tUTS, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addGap(26, 26, 26)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                            .addComponent(tUAS, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                            .addComponent(jLabel12))))
                .addGap(35, 35, 35))
        );

        jLabel1.setFont(new java.awt.Font("Tahoma", 0, 18));
        jLabel1.setText("Input Nilai Mahasiswa");

        javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
        jPanel1.setLayout(jPanel1Layout);
        jPanel1Layout.setHorizontalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jSeparator1, javax.swing.GroupLayout.DEFAULT_SIZE, 250, Short.MAX_VALUE)
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addComponent(jLabel1)
                        .addGap(60, 78, Short.MAX_VALUE)))
                .addContainerGap())
        );
        jPanel1Layout.setVerticalGroup(
            jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel1Layout.createSequentialGroup()
                .addComponent(jLabel1)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addComponent(jSeparator1, javax.swing.GroupLayout.PREFERRED_SIZE, 10, javax.swing.GroupLayout.PREFERRED_SIZE))
        );

        jlMahasiswa.addListSelectionListener(new javax.swing.event.ListSelectionListener() {
            public void valueChanged(javax.swing.event.ListSelectionEvent evt) {
                jlMahasiswaValueChanged(evt);
            }
        });
        jScrollPane2.setViewportView(jlMahasiswa);

        TbMahasiswa.setModel(new javax.swing.table.DefaultTableModel(
            new Object [][] {
                {null, null, null, null, null, null, null, null, null},
                {null, null, null, null, null, null, null, null, null},
                {null, null, null, null, null, null, null, null, null},
                {null, null, null, null, null, null, null, null, null}
            },
            new String [] {
                "NRP", "Nama", "Tingkat", "Jurusan", "Program Studi", "Tugas", "Kuis", "UTS", "UAS"
            }
        ));
        TbMahasiswa.addMouseListener(new java.awt.event.MouseAdapter() {
            public void mousePressed(java.awt.event.MouseEvent evt) {
                TbMahasiswaMousePressed(evt);
            }
        });
        jScrollPane1.setViewportView(TbMahasiswa);

        btSimpan.setText("Simpan");
        btSimpan.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                btSimpanActionPerformed(evt);
            }
        });

        btHapus.setText("Hapus");

        javax.swing.GroupLayout jPanel4Layout = new javax.swing.GroupLayout(jPanel4);
        jPanel4.setLayout(jPanel4Layout);
        jPanel4Layout.setHorizontalGroup(
            jPanel4Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel4Layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(jPanel4Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(jScrollPane1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(jScrollPane2, javax.swing.GroupLayout.DEFAULT_SIZE, 452, Short.MAX_VALUE)
                    .addGroup(jPanel4Layout.createSequentialGroup()
                        .addComponent(btSimpan)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                        .addComponent(btHapus)))
                .addContainerGap())
        );
        jPanel4Layout.setVerticalGroup(
            jPanel4Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(jPanel4Layout.createSequentialGroup()
                .addContainerGap()
                .addComponent(jScrollPane2, javax.swing.GroupLayout.PREFERRED_SIZE, 145, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                .addComponent(jScrollPane1, javax.swing.GroupLayout.PREFERRED_SIZE, 135, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(18, 18, 18)
                .addGroup(jPanel4Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(btSimpan)
                    .addComponent(btHapus))
                .addContainerGap(22, Short.MAX_VALUE))
        );

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addContainerGap()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING, false)
                    .addComponent(jPanel2, javax.swing.GroupLayout.Alignment.LEADING, 0, 270, Short.MAX_VALUE)
                    .addComponent(jPanel1, javax.swing.GroupLayout.Alignment.LEADING, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                .addGap(18, 18, 18)
                .addComponent(jPanel4, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING, false)
                    .addGroup(javax.swing.GroupLayout.Alignment.LEADING, layout.createSequentialGroup()
                        .addGap(66, 66, 66)
                        .addComponent(jPanel4, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                    .addGroup(javax.swing.GroupLayout.Alignment.LEADING, layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)))
                .addContainerGap(23, Short.MAX_VALUE))
        );
    }// </editor-fold>                        

private void cProgramStudiItemStateChanged(java.awt.event.ItemEvent evt) {                                               
if(cProgramStudi.getSelectedIndex() == 0){
            cKonsentrasi.removeAllItems();
        }
        else if(cProgramStudi.getSelectedIndex() == 1){
            cKonsentrasi.removeAllItems();
            cKonsentrasi.addItem("Sekretaris");
            cKonsentrasi.addItem("Manajemen");
        }
        else if(cProgramStudi.getSelectedIndex() == 2){
            cKonsentrasi.removeAllItems();
            cKonsentrasi.addItem("Komputer Akuntansi");
            cKonsentrasi.addItem("Perpajakan");
        }
        else if(cProgramStudi.getSelectedIndex() == 3){
            cKonsentrasi.removeAllItems();
            cKonsentrasi.addItem("Teknik Informatika");
            cKonsentrasi.addItem("Manajemen Informatika");
        }            // TODO add your handling code here:
        
           
}                                              

                                  

private void jlMahasiswaValueChanged(javax.swing.event.ListSelectionEvent evt) {                                         
  if(jlMahasiswa.getSelectedIndex() >= 0){
            selectedMahasiswa = lsMahasiswa.get(jlMahasiswa.getSelectedIndex());
        }
        
        //refreshDetailNilai();        
      
}                                        

private void TbMahasiswaMousePressed(java.awt.event.MouseEvent evt) {                                         
  if(TbMahasiswa.getSelectedRow() >= 0){
            selectedMahasiswa = lsMahasiswa.get(TbMahasiswa.getSelectedRow());
        }
        refreshDetailNilai();
       
}                                        

                                 

private void btSimpanActionPerformed(java.awt.event.ActionEvent evt) {                                         
boolean simpan = true;

        /*if(myCon.isDuplicate(tNoRegistrasi.getText())){
            JOptionPane.showMessageDialog(this, "No. Registrasi sudah digunakan!");
            simpan = false;
        }
        else*/ if(tNama.getText().length() == 0){
            JOptionPane.showMessageDialog(this, "Silahkan isi nama lengkap mahasiswa!");
            simpan = false;
        }
        else if (tnrp.getText().length()==0){
            JOptionPane.showMessageDialog(this, "Silahkan isi NRP!");
            simpan = false;
        }
         else if (tTugas.getText().length()==0){
            JOptionPane.showMessageDialog(this, "Silahkan isi Nilai Tugas!");
            simpan = false;
        }
          else if (tUAS.getText().length()==0){
            JOptionPane.showMessageDialog(this, "Silahkan isi Nilai UAS!");
            simpan = false;
        }
           else if (tUTS.getText().length()==0){
            JOptionPane.showMessageDialog(this, "Silahkan isi Nilai UTS!");
            simpan = false;
        }
            else if (tKuis.getText().length()==0){
            JOptionPane.showMessageDialog(this, "Silahkan isi Nilai KUIS!");
            simpan = false;
        }
        else if(cProgramStudi.getSelectedIndex() == 0){
            JOptionPane.showMessageDialog(this, "Silahkan pilih program studi!");
            simpan = false;
        } else if(cKonsentrasi.getSelectedIndex() == 0){
            JOptionPane.showMessageDialog(this, "Silahkan pilih Konsentrasi!");
            simpan = false;
        }
        
             
        
        if(simpan){
            ListField m = new ListField();
            
            m.setnrp(tnrp.getText());
            m.setnama(tNama.getText());
            m.settingkat(cTingkat.getSelectedItem().toString());
            m.setprogramstudi(cTingkat.getSelectedItem().toString());
            m.setkonsentrasi(cKonsentrasi.getSelectedItem().toString());
            m.settugas(tTugas.getText());
            m.setkuis(tKuis.getText());
            m.setuts(tUTS.getText());
            m.setuas(tUAS.getText());
            
           

            if(!myCon.isDuplicate(m.getnrp()))
                myCon.insertnilai(m);
            else
                myCon.updateMahasiswa(m);
            
            clean();
            init();
            refreshnilai();
            refreshnilaiontable();
            refreshDetailNilai();
           }
}                                        
private void formInputMethodTextChanged(java.awt.event.InputMethodEvent evt) {                                            


}                                           
 public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(JForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(JForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(JForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(JForm.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new JForm().setVisible(true);
            }
        });
    }
    // Variables declaration - do not modify                     
    private javax.swing.JTable TbMahasiswa;
    private javax.swing.JButton btHapus;
    private javax.swing.JButton btSimpan;
    private javax.swing.JComboBox cKonsentrasi;
    private javax.swing.JComboBox cProgramStudi;
    private javax.swing.JComboBox cTingkat;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel10;
    private javax.swing.JLabel jLabel11;
    private javax.swing.JLabel jLabel12;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JLabel jLabel3;
    private javax.swing.JLabel jLabel4;
    private javax.swing.JLabel jLabel5;
    private javax.swing.JLabel jLabel6;
    private javax.swing.JLabel jLabel7;
    private javax.swing.JLabel jLabel8;
    private javax.swing.JLabel jLabel9;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel jPanel2;
    private javax.swing.JPanel jPanel3;
    private javax.swing.JPanel jPanel4;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JScrollPane jScrollPane2;
    private javax.swing.JSeparator jSeparator1;
    private javax.swing.JSeparator jSeparator2;
    private javax.swing.JSeparator jSeparator3;
    private javax.swing.JSeparator jSeparator4;
    private javax.swing.JSeparator jSeparator5;
    private javax.swing.JList jlMahasiswa;
    private javax.swing.JTextField tKuis;
    private javax.swing.JTextField tNama;
    private javax.swing.JTextField tTugas;
    private javax.swing.JTextField tUAS;
    private javax.swing.JTextField tUTS;
    private javax.swing.JTextField tnrp;
    // End of variables declaration                   

  
}

