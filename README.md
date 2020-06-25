# Wanderson-Gui-Documentation
Wanderson Gui Documentation


I'm not the owner/developer of this gui.
Check his channel: https://www.youtube.com/user/VFXtestingWMP


# Documentation

# Heading 1 #


**Table of Contents**

- [Example 1 Heading](###Modify the gui)




###Modify the gui ###

                
----
In order to modify the gui you need to install PyQt Designer or PySide2 Designer

`pip install PyQt5`
	[Link to PyQt5](https://pypi.org/project/PyQt5/ "Link to PyQt5")
	
or

`pip install PySide2`
[Link to PySide2](https://pypi.org/project/PySide2/ "Link to PySide2")
####Change the current page ####

To change the current page we must click the two arrows on the top right of the stacked widget.
[![Change Current Page](https://i.imgur.com/w6Tk8WK.png "Change Current Page")](https://i.imgur.com/w6Tk8WK.png "Change Current Page")

####Add a new page ####

To add a new page,  right click on stacked widget in the object inspector -> Insert Page -> Choose the order you prefer

[![Add New Page](https://i.imgur.com/SQue5Ue.png "Add New Page")](https://i.imgur.com/SQue5Ue.png "Add New Page")


####Add a new menu button ####


[![Add New Button](https://i.imgur.com/zIdhiID.png "Add New Button")](https://i.imgur.com/zIdhiID.png "Add New Button")

To add a new menu button open the main.py and search for `## ==> ADD CUSTOM MENUS` comment and add a new line `UIFunctions.addNewMenu(self, "TEXT_DISPLAYED_IN_THE_GUI", "NAME_OF_THE_BUTTON", "url(:/16x16/icons/16x16/cil-home.png)", True)`

For better uderstanding of the method let's look the code:


        def addNewMenu(self, name, objName, icon, isTopMenu):
        	font = QFont()
        	font.setFamily(u"Segoe UI")
        	button = QPushButton(str(count),self)
        	button.setObjectName(objName)
			sizePolicy3 = QSizePolicy(QSizePolicy.Expanding, QSizePolicy.Fixed)
			sizePolicy3.setHorizontalStretch(0)
			sizePolicy3.setVerticalStretch(0)
			sizePolicy3.setHeightForWidth(button.sizePolicy().hasHeightForWidth())
			button.setSizePolicy(sizePolicy3)
			button.setMinimumSize(QSize(0, 70))
			button.setLayoutDirection(Qt.LeftToRight)
			button.setFont(font)
			button.setStyleSheet(Style.style_bt_standard.replace('ICON_REPLACE', icon))

			button.setText(name)
			button.setToolTip(name)
			button.clicked.connect(self.Button)

			if isTopMenu:
				self.ui.layout_menus.addWidget(button)
			else:
				self.ui.layout_menu_bottom.addWidget(button)


Parameters:

`name` - > Name displayed in the gui.
`objName` -> The name of the button.
`icon` The url for the icon, see your folder icons and you will understand.
`isTopMenu`  To set the button under the user logo -> False -> to set above -> True

Example:
`UIFunctions.addNewMenu(self, "My Page", "btn_my_page", "url(:/16x16/icons/16x16/cil-home.png)", True)`

####Select the page to display when the button is pressed ####

Search the `## MENUS ==> DYNAMIC MENUS FUNCTIONS` comment

Add the code:
        
	if btnWidget.objectName() == "btn_my_page":
		self.ui.stackedWidget.setCurrentWidget(self.ui.my_page)
		UIFunctions.resetStyle(self, "btn_widgets")
		UIFunctions.labelPage(self, "Custom Widgets")
		btnWidget.setStyleSheet(UIFunctions.selectMenu(btnWidget.styleSheet()))
		
		
		`self.ui.my_page` change it to the name of the page you given when you added a 
		new page to the stacked widget
		
#Save your .ui file and convert it to a .py file #
###Save and convert ###

File -> Save As... when you saved go to your folder and open the Terminal/Command Prompt inside it then write `pyuic5 your_gui_file.ui -o your_gui_file_py`.

###Import your new ui in main.py ###

Search the comment `# GUI FILE` and change `from ui_main_modified import Ui_MainWindow` to `from your_gui_file import Ui_MainWindow`

####Fixing the errors on your new gui file ####

To do that just replace avery import from `PyQt5` to `PySide2` and add 
`from PySide2 import QtGui, QtCore, QtWidgets`








