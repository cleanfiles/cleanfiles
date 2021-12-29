- 👋 Hi, I’m @cleanfiles
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
cleanfiles/cleanfiles is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
/*
 * Created by SharpDevelop.
 * User: ASUS
 * Date: 12/29/2021
 * Time: 10:06 PM
 * 
 * To change this template use Tools | Options | Coding | Edit Standard Headers.
 */
using System;
using Autodesk.Revit.UI;
using Autodesk.Revit.DB;
using Autodesk.Revit.UI.Selection;
using System.Collections.Generic;
using System.Linq;

namespace cleanfiles
{
	[Autodesk.Revit.Attributes.Transaction(Autodesk.Revit.Attributes.TransactionMode.Manual)]
	[Autodesk.Revit.DB.Macros.AddInId("EE7FB93B-5CC2-40AF-9944-31822355B433")]
	public partial class ThisApplication
	{
		private void Module_Startup(object sender, EventArgs e)
		{

		}

		private void Module_Shutdown(object sender, EventArgs e)
		{

		}

		#region Revit Macros generated code
		private void InternalStartup()
		{
			this.Startup += new System.EventHandler(Module_Startup);
			this.Shutdown += new System.EventHandler(Module_Shutdown);
		}
		#endregion
		
		
		public void jiren1()
		{
			Document doc=this.ActiveUIDocument.Document;
			IList<Element> list=this.ActiveUIDocument.Selection.PickElementsByRectangle();
			IList<Element> list1=new List<Element>();
			for (int i =0 ; i < list.Count;i++)
			{
				BoundingBoxXYZ bb = list[i].get_BoundingBox(null);
				double z = bb.Max.X;
				Element e=null;
				for(int j =i+1;j<list.Count;j++)
				{
					BoundingBoxXYZ bb1 = list[j].get_BoundingBox(null);
					double x = bb1.Max.X;
					if(z > x)
					{
						z = x;
						e = list[j];
						list[j] = list[i];
					}
				}
				list1.Add(e);
			}
			Transaction t=new Transaction(doc,"revit");
			t.Start();
			
			for (int i = 0; i < list1.Count; i++)
			{
				string name ="100.C"+ Convert.ToString(i);
				list[i].LookupParameter("Comments").Set(name);
				
			}
			
			
			t.Commit();
			
			
		}
	}
}
