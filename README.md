# JAVA-IO

A. Streams

byte oriented stream (8 bit)
good for binary data such as a Java .class file
good for "machine-oriented"

B. Readers/Writers

char (utf-16) oriented stream (16 bit)
good for text such as a Java source
good for "human-oriented" data
Buffered

C. always useful unless proven otherwise

For Streams:
   1. InputStream vs OutputStream
    a.InputStream is used for many things that you read from.
    ex: an method that can read from an existing file(read byte one by one):
    
      public static void printlnHex(String fileName) throws IOException{
		//convert file into a stream and do read operation
		FileInputStream in = new FileInputStream(fileName);
		int b;
		int i =1;
		while((b=in.read())!=-1){
		//	System.out.println(b);
		//	System.out.println("16Hex");
			
			System.out.println(Integer.toHexString(b)+ " ");
			System.out.println("println i");
			if(i++%10==0){
				System.out.println();
			}
		}
		 in.close();
	}
	
	an method that can read form an existing file(read by bytes array)
	public static void printlnHexByByteArray(String fileName) throws IOException{
		
			FileInputStream in = new FileInputStream(fileName);
			byte[] buf = new byte[20*1024];
			// 从in中批量读取字节，放入buf中，从第0
			//个开始放，最多放buf.length 个 返回的是读到的字节个数。
			int bytes = in.read(buf, 0, buf.length);
			for(int i=0;i< bytes;i++){
				System.out.println(Integer.toHexString(buf[i]));
			}
			in.close();
	}
		

   b. OutputStream is used for many things that you write to.
    
    ex: FileOutputStream out = new FileOutputStream("/Users/KevinZheng/Documents/workspace/JavaIO/KevinZheng.txt");
      //write single bytes into file
			out.write('A');
			out.write('B');
			//write byte array into file
			byte[] gbk = "China".getBytes("gbk");
			out.write(gbk);
			
    c.Copy a scrfile to a desfile:
	
	public static void copyFile(File srcfile, File desfile) throws IOException{
		if(!srcfile.exists()){
			throw new IllegalArgumentException("file" + srcfile + "does not exist.");
		}
		
		if(!srcfile.isFile()){
			throw new IllegalArgumentException( srcfile + "is not a file");
		}
		
		@SuppressWarnings("resource")
		FileInputStream in = new FileInputStream(srcfile);
		@SuppressWarnings("resource")
		FileOutputStream out = new FileOutputStream(desfile);
		byte[] buf = new byte[8*1024];
		int b;
		while((b=in.read(buf,0, buf.length))!=-1){
			out.write(buf, 0, b);
		}
		
	}
