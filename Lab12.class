import java.io.File;
import java.io.FileNotFoundException;
import java.util.HashMap;
import java.util.Hashtable;
import java.util.Scanner;
import java.util.Map;
import java.util.Enumeration;

public class DataManager {
	private String fileLocation="";
	String[] dates;
	String[] states;
	String[] countries;
	// int[][] data;
	Map<String, Hashtable<String, Hashtable<String, Integer>>> data = new HashMap<String, Hashtable<String, Hashtable<String, Integer>>>();//hash
	public DataManager(String fileLocation) {
		this.setFileLocation(fileLocation);
		try {
			int n=0;
			Scanner in = new Scanner(new File(fileLocation));
			dates=in.nextLine().strip().substring(39).split(",");

			while(in.hasNext()){
				// System.out.println(in.nextLine());
				in.nextLine();
				n++;
			}
			in.close();
			states=new String[n];
			countries=new String[n];
			// data = new int[
			in = new Scanner(new File(fileLocation));
			in.nextLine().strip();
			int line=0;
			while(in.hasNext()){
				// System.out.println(in.nextLine());
				String[] tokens=in.nextLine().strip().split(",");
				// System.out.println(tokens[0].equals(""));
				states[line]=tokens[0];
				countries[line]=tokens[1];
				Hashtable<String, Integer> temp = new Hashtable<String, Integer>(); // hash
				for(int i=4;i<tokens.length;i++) {
					// data[line][i-4]=Integer.parseInt(tokens[i]);
					temp.put(dates[i - 4], Integer.parseInt(tokens[i])); // hash
					// System.out.println(dates[i - 4]);
				}
				Hashtable<String, Hashtable<String, Integer>> temp2 = new Hashtable<String, Hashtable<String, Integer>>();

				temp2.put(tokens[0], temp);
				if(!data.containsKey(tokens[1]))
					data.put(tokens[1], temp2);
				else
					data.get(tokens[1]).put(tokens[0], temp);
				line++;
			}
			in.close();
		}
		catch(FileNotFoundException ex) {
			System.out.println("File not found.");
			fileLocation="";
		}
		
	}
	private int getIndex(String[] arrayIn,String key) {
		for(int i=0;i<arrayIn.length;i++) {
			if(arrayIn[i].equalsIgnoreCase(key)) {
				return i;
			}
		}
		return -1;
	}
	public int getData(String state,String country,String date) {
		if(state.equals("")) {
			int sum=0;
			Enumeration<String> enumeration = data.get(country).keys();

			while(enumeration.hasMoreElements()) {
				String key = enumeration.nextElement();
				// System.out.println(key);
				sum+=data.get(country).get(key).get(date);
			}
			return sum;
		}
		int ans = data.get(country).get(state).get(date);
		return ans;
	}

	// public int getData(String state,String country,String date) {
	// 	if(state.equals("")) {
	// 		int sum=0;
	// 		for(int i=0;i<this.states.length;i++) {
	// 			if(countries[i].equalsIgnoreCase(country)) {
	// 				int ind=getIndex(dates,date);
	// 				if(ind != -1) {
	// 					sum += data[i][ind];
	// 				}
	// 			}
	// 		}
	// 		return sum;
	// 	}
	// 	int stateIndex=getIndex(states,state);
	// 	int dateIndex=getIndex(dates,date);
	// 	return data[stateIndex][dateIndex];
	// }
	public String getFileLocation() {
		return fileLocation;
	}
	public void setFileLocation(String fileLocation) {
		this.fileLocation = fileLocation;
	}
}
