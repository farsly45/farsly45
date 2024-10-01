import ui
import app
import time
import chr
import math
import Jsg as ime
import item
import os
import sys
import dbg
import uiAuto
import mouseModule
import uiRestart
import uiCharacter
import HEWa as shop
import uiCommon
import uiTarget
import introSelect
import networkModule
import introLogin
import event
import game
import playerm2g2 as player
import chatm2g as chat
import m2netm2g as net
import constInfo
import functools
import historysml
import background

minyang = 4000000
bazaarStat = 0
yang = 0
NpcName = "Alchemist"
listEnergySlot = [91]
OldRecv = game.GameWindow.OpenQuestWindow
tradeAdminCoorTA = 27703,25281,16383
tradeAdminCoorRV1 = 68335,58078,19866
SellerRV1 = 67600,56500,19866
WeaponDealerRV1 = 59614,56058,19839
AlchemistRV1 = 62697,50655,19862.5
SellAreaCoor = 22343,33009,16407
NpcMarketCoorTA = 36048,31652,16383
redVillage1 = "metin2_map_a1"
tradeMap = "metin2_map_privateshop"
energymode = 0
roadonv1mode = 0
clicked = 0
timerweapondelar = 0
waitontrd = 0
sellmode = 0
debugtime= 0
steppedcount = 0
rv1clicked = 0
moveWaiterMap1Energy = 0
moveWaiterMap1Trade = 0
moneycheck = 0
needpacket = 0
pagecheck = 0
needenergy = 0
searchstat = 0
pagenumber = 1
priceokey = 0
lastcheck = 10000000



def Log(data):
    chat.AppendChat(7, str(data))


class mini(ui.ScriptWindow):
    visible = 1
    otoenergy = 0
    otobazaar = 0
    rotate = 0
    aulog = 0
    eysan = 0
    kerpetenali = 'None'
    isConnected = 0
    getatoni = None
    otodrop = 0
    otoenergyremover = 0


    def __init__(self):
        ui.ScriptWindow.__init__(self)
        self.dlgQuestion = None
        thinBoard = ui.ThinBoard()
        thinBoard.SetSize(316, 253)
        thinBoard.SetCenterPosition()
        thinBoard.AddFlag('movable')
        thinBoard.Show()
        self.thinBoard = thinBoard
        form = ui.ExpandedImageBox()
        form.SetParent(self.thinBoard)
        form.AddFlag('attach')
        form.AddFlag('not_pick')
        form.AddFlag('movable')
        form.SetPosition(-2, -1)
        form.SetWindowVerticalAlignCenter()
        form.SetWindowHorizontalAlignCenter()
        form.Show()
        self.form = form
        self.form.LoadImage('lib/unxgui/form.tga')
        tabPage1 = ui.ExpandedImageBox()
        tabPage1.SetParent(self.form)
        tabPage1.AddFlag('attach')
        tabPage1.AddFlag('not_pick')
        tabPage1.SetPosition(-1, 28)
        tabPage1.SetWindowVerticalAlignCenter()
        tabPage1.SetWindowHorizontalAlignCenter()
        tabPage1.Show()
        self.tabPage1 = tabPage1
        self.tabPage1.LoadImage('lib/unxgui/tabPage.tga')
        tabPage2 = ui.ExpandedImageBox()
        tabPage2.SetParent(self.form)
        tabPage2.AddFlag('attach')
        tabPage2.AddFlag('not_pick')
        tabPage2.SetPosition(-1, 28)
        tabPage2.SetWindowVerticalAlignCenter()
        tabPage2.SetWindowHorizontalAlignCenter()
        tabPage2.Hide()
        self.tabPage2 = tabPage2
        self.tabPage2.LoadImage('lib/unxgui/tabPage.tga')
        self.comp = Component()
        self.formTitle = self.comp.TextLine(self.form, '-lexa2023 & DadyBlue Botting Cooperation "All Rights Reserved"', 30, 5, self.comp.RGB(223, 160, 109))
        self.ClsBtn = self.comp.Button(self.form, '', 'Press [F2] to show window', 307, 4, self.Cls, 'lib/unxgui/panelclose0.tga', 'lib/unxgui/panelclose1.tga', 'lib/unxgui/panelclose0.tga')
        self.tabBtn1 = self.comp.ToggleButton(self.form, 'Energy Bot', '', 15, 40, self.SetTabPage1, self.SetTabPage1, 'lib/unxgui/tabBtn0b.tga', 'lib/unxgui/tabBtn0.tga', 'lib/unxgui/tabBtn1.tga')
        self.tabBtn2 = self.comp.ToggleButton(self.form, 'Shop Bot', '', 87, 40, self.SetTabPage2, self.SetTabPage2, 'lib/unxgui/tabBtn0b.tga', 'lib/unxgui/tabBtn0.tga', 'lib/unxgui/tabBtn1.tga')
        self.EnergyCrafter = self.comp.ToggleButton(self.tabPage1, '', 'Enerji Uret', 25, 25, self.EnergyCrafter0, self.EnergyCrafter1, 'lib/unxgui/refine0.tga', 'lib/unxgui/refine1.tga', 'lib/unxgui/refine2.tga')
        self.EnergyCrafter2 = self.comp.ToggleButton(self.tabPage1, '', 'Yere At', 65, 25, self.EnergyRemover0, self.EnergyRemover1, 'lib/unxgui/boost0.tga', 'lib/unxgui/boost1.tga', 'lib/unxgui/boost2.tga')
        self.DoCamBtn = self.comp.Button(self.tabPage1, '', 'Rotate Camera', 105, 25, self.DoRotate, 'lib/unxgui/cam1.tga', 'lib/unxgui/cam2.tga', 'lib/unxgui/cam1.tga')
        self.SetTabPage1()
        self.Energyle()
        self.EnergyRemove()
        self.DropInvtime()
        return

    def Cls(self):
        self.thinBoard.Hide()
        self.visible = 0

    def SetTabPage1(self):
        self.tabPage1.Show()
        self.tabPage2.Hide()
        self.tabBtn1.Down()
        self.tabBtn2.SetUp()

    def SetTabPage2(self):
        self.tabPage2.Show()
        self.tabPage1.Hide()
        self.tabBtn2.Down()
        self.tabBtn1.SetUp()




    def EnergyCrafter0(self):
        self.otoenergy = 0

    def EnergyCrafter1(self):
        self.otoenergy = 1

    def Dropper0(self):
        self.otodrop = 0

    def Dropper1(self):
        self.otodrop = 1

    def EnergyRemover0(self):
        self.otoenergyremover = 0

    def EnergyRemover1(self):
        self.otoenergyremover = 1


    

    
    def Energyle(self):
        if self.otoenergy== 1:
            MainLoop()
        self.energydelay = Delay()
        self.energydelay.Open(float(0.3))
        self.energydelay.SAFE_SetTimeOverEvent(self.Energyle)

    def EnergyRemove(self):
        if self.otoenergyremover== 1:
            Log("Hello")
        self.energydelayremover = Delay()
        self.energydelayremover.Open(float(0.3))
        self.energydelayremover.SAFE_SetTimeOverEvent(self.EnergyRemove)




    def DoRotate(self):
        if self.rotate == 0:
            self.rotate = 1
            app.MovieRotateCamera(app.CAMERA_TO_POSITIVE)
            UnHookQuestWindow()
        else:
            self.rotate = 0
            app.MovieRotateCamera(app.CAMERA_STOP)
            UnHookQuestWindow()


    def DropInvtime(self):
        if self.otodrop== 1:
            ListOfEnergyFragment()
        self.energydelay2 = Delay()
        self.energydelay2.Open(float(0.3))
        self.energydelay2.SAFE_SetTimeOverEvent(self.DropInvtime)






    


    
    
  



    

    


class Component():

    def Button(self, parent, buttonName, tooltipText, x, y, func, UpVisual, OverVisual, DownVisual):
        button = ui.Button()
        if parent != None:
            button.SetParent(parent)
        button.SetPosition(x, y)
        button.SetUpVisual(UpVisual)
        button.SetOverVisual(OverVisual)
        button.SetDownVisual(DownVisual)
        button.SetText(buttonName)
        button.SetToolTipText(tooltipText)
        button.Show()
        button.SetEvent(func)
        return button

    def ToggleButton(self, parent, buttonName, tooltipText, x, y, funcUp, funcDown, UpVisual, OverVisual, DownVisual):
        button = ui.ToggleButton()
        if parent != None:
            button.SetParent(parent)
        button.SetPosition(x, y)
        button.SetUpVisual(UpVisual)
        button.SetOverVisual(OverVisual)
        button.SetDownVisual(DownVisual)
        button.SetText(buttonName)
        button.SetToolTipText(tooltipText)
        button.Show()
        button.SetToggleUpEvent(funcUp)
        button.SetToggleDownEvent(funcDown)
        return button

    def TextLine(self, parent, textlineText, x, y, color):
        textline = ui.TextLine()
        if parent != None:
            textline.SetParent(parent)
        textline.SetPosition(x, y)
        if color != None:
            textline.SetFontColor(color[0], color[1], color[2])
        textline.SetText(textlineText)
        textline.SetOutline()
        textline.Show()
        return textline

    def RGB(self, r, g, b):
        return (r * 255, g * 255, b * 255)

    def ExpandedImage(self, parent, x, y, img):
        image = ui.ExpandedImageBox()
        if parent != None:
            image.SetParent(parent)
        image.SetPosition(x, y)
        image.LoadImage(img)
        image.Show()
        return image

    def ThinBoard(self, parent, moveable, x, y, width, heigh, center):
        thin = ui.ThinBoard()
        if parent != None:
            thin.SetParent(parent)
        if moveable == TRUE:
            thin.AddFlag('movable')
            thin.AddFlag('float')
        thin.SetSize(width, heigh)
        thin.SetPosition(x, y)
        if center == TRUE:
            thin.SetCenterPosition()
        thin.Show()
        return thin


class Delay(ui.ScriptWindow):

    def __init__(self):
        ui.ScriptWindow.__init__(self)
        self.eventTimeOver = lambda *arg: None
        self.eventExit = lambda *arg: None

    def __del__(self):
        ui.ScriptWindow.__del__(self)

    def Open(self, waitTime):
        curTime = time.clock()
        self.endTime = curTime + waitTime
        self.Show()

    def Close(self):
        self.Hide()

    def SAFE_SetTimeOverEvent(self, event):
        self.eventTimeOver = ui.__mem_func__(event)

    def SAFE_SetExitEvent(self, event):
        self.eventExit = ui.__mem_func__(event)

    def OnUpdate(self):
        lastTime = max(0, self.endTime - time.clock())
        if 0 == lastTime:
            self.Close()
            self.eventTimeOver()
        else:
            return

    def OnPressExitKey(self):
        self.Close()
        return TRUE

class Hook():
	"""
	Hook class that allows to replace functions in modules.
	"""
	def __init__(self,toHookFunc,replaceFunc):
		self.originalFunc = toHookFunc
		self.replaceFunc = replaceFunc
		self.functionName = str(toHookFunc.__name__)
		self.functionOwner = self.GetFunctionOwner(toHookFunc)
		self.isHooked = False



	def GetFunctionOwner(self,func):
		"""
		Return the object owner of the function 

		Args:
			func ([function]): a function.

		Returns:
			[object]: Return the object owner of the function.
		"""
		try:
			owner = func.im_class		#In case of a class function
		except AttributeError:
			owner = sys.modules[func.__module__]
		
		return owner


	def CallOriginalFunction(self,*args,**kwargs):
		"""
		Call the original function before the hook.
		Returns:
			[args]: the arguments of the function.
		"""
		@functools.wraps(self.originalFunc)
		def run(*args, **kwargs):
			return self.originalFunc(*args, **kwargs)
		return run(*args,**kwargs)
		
	def HookFunction(self):
		"""
		Hook the function.
		"""
		if self.isHooked:
			return
		self.isHooked = True
		setattr(self.functionOwner, self.functionName, self.replaceFunc)

	def UnhookFunction(self):
		"""
		Remove the hook and put the original function.
		"""
		if self.isHooked == False:
			return
		self.isHooked = False
		#chat.AppendChat(3,"Function Owner: " + str(self.functionOwner.__name__) + "Function Name: " + str(self.functionName))
		setattr(self.functionOwner, self.functionName, self.originalFunc)

    




minicls = mini()
minicls.Show()






def ClickTheNpc(a):
	for vid in range(100000):
		if chr.GetNameByVID(vid) == a:
			net.SendOnClickPacket(vid)


def ListOfEnergyFragment():
    global listEnergySlot
    for i in range (90):
        if player.GetItemIndex(i) == 51001 and player.GetItemCount(i) == 200:
            listEnergySlot.append(i)
    for y in listEnergySlot:
        if 2 <= listEnergySlot.count(y) :
            listEnergySlot.remove(y)
    for z in range(90):
            if not player.GetItemIndex(z) == 51001 and (z in listEnergySlot):
                listEnergySlot.remove(z)

    Log(listEnergySlot)
    Log("d0ru")
    Log(historysml.moveWaiterTrd1)
    Log(historysml.moveWaiterTrd2)
    Log(historysml.moveWaiterTrd3)
    Log(historysml.moveWaiterTrd4)
    Log(historysml.moveWaiterTrd5)

def InstallQuestWindowHook():

	try:
		if constInfo.QuestOld == "":

			constInfo.QuestOld = game.GameWindow.OpenQuestWindow

	except:

		constInfo.QuestOld = ""
	
	if constInfo.QuestOld == "":

		constInfo.QuestOld = game.GameWindow.OpenQuestWindow

	game.GameWindow.OpenQuestWindow = HookedQuestWindow

def UnHookQuestWindow():
	game.GameWindow.OpenQuestWindow = constInfo.QuestOld

def HookedQuestWindow(self, skin, idx):
	pass

def isInventoryFull():
    global player
    INV_FULL_MIN_EMPTY = 10
    MAX_INVENTORY_SIZE = 90

    numItems = MAX_INVENTORY_SIZE
    for i in range(0,MAX_INVENTORY_SIZE):
        curr_id = player.GetItemIndex(i)
        if curr_id != 0:
            item.SelectItem(curr_id)
            s = item.GetItemSize()
            numItems-=s[0]*s[1]

    if numItems < INV_FULL_MIN_EMPTY:
        return True
    else:
        return False

def Scan_Npc(name):
	npc = -1
	for i in range(50000):
		if chr.GetNameByVID(int(i)) == name:	
			npc = i
			break
	return npc

alchid = Scan_Npc(NpcName)

def DaggerToEnergy():
    
	for i in range(90):	
		if (player.GetItemIndex(i) == 1040):
				net.SendGiveItemPacket(alchid, i, 1) 
				event.SelectAnswer(1,0)
				event.SelectAnswer(1,0)

def DaggerToEnergy2():
    global alchid2 
    alchid2 = -1
    InstallQuestWindowHook()
    for z in range(50000):
        if chr.GetNameByVID(int(z)) == "Alchemist":
            alchid2 = z
    
    for i in range(90):
        if player.GetItemIndex(i) == 1040:
            net.SendGiveItemPacket(alchid2,i,1)
            event.SelectAnswer(1,0)
            event.SelectAnswer(1,0)
    

def WeaponDealerToAlchemy():
    chr.SetPixelPosition(59614.1328125,56058.54296875,19839.818359375) 
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(61037.26171875,55881.58203125,19862.5)
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(61016.70703125,53936.4375,19867.107421875)
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(61861.46484375,52641.62109375,19867.357421875) 
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(62397,50955,19862.5) 
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)

def AlchemyToWeaponDealer():
    chr.SetPixelPosition(62397,50955,19862.5)
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(61861.46484375,52641.62109375,19867.357421875)
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W) 
    chr.SetPixelPosition(61016.70703125,53936.4375,19867.107421875)
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(61037.26171875,55881.58203125,19862.5) 
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    chr.SetPixelPosition(59614.1328125,56058.54296875,19839.818359375) 
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)



def EnergyBot():
    x,y,z = player.GetMainCharacterPosition()
    if(not 59000.0000000 < x < 60000.0000000):
        AlchemyToWeaponDealer()
    if(isInventoryFull() == False and player.GetMoney() >= 100000):
        if(shop.IsOpen() == 0 ):
            InstallQuestWindowHook()
            ClickTheNpc("Weapon Shop Dealer")
            
            event.SelectAnswer(0,1)
            event.SelectAnswer(1,254)
            event.SelectAnswer(1,1)
           
            
        elif(isInventoryFull() == False):
            net.SendShopBuyPacket   (4, 0, 1)
    elif(isInventoryFull() == True):
        WeaponDealerToAlchemy()
        DaggerToEnergy2()
    

def DropInv():   
    for x in range (90):
        net.SendItemDropPacketNew(x,0)

def HotkeyRelog():
    if app.IsPressed(app.DIK_F2) and minicls.visible == 0:
        minicls.visible = 1
        minicls.thinBoard.Show()


hrlg = ui.Window()
hrlg.OnUpdate = HotkeyRelog
hrlg.Show()

def TimeToGo(DesX , DesY , DesZ):
    global mx
    global my
    global mz
    mx, my, mz = player.GetMainCharacterPosition()
    
   
    if mx != DesX and abs(mx-DesX) >= 101 and mx > DesX :
        chr.SetPixelPosition((mx-100),my,DesZ)
        
        DebugW()
        

    elif mx != DesX and abs(mx-DesX) >= 101 and mx < DesX :
        chr.SetPixelPosition((mx+100),my,DesZ)
        DebugW()

    if my != DesY and abs(my-DesY) >= 101 and my < DesY :
        chr.SetPixelPosition(mx,(my+100),DesZ)
        DebugW()

    elif my != DesY and abs(my-DesY) >= 101 and my > DesY :
        chr.SetPixelPosition(mx,(my-100),DesZ)
        DebugW()


def DebugW():
    player.OnKeyDown(app.DIK_W)
    player.OnKeyUp(app.DIK_W)
    
def HaveAnEnergy():
    INV_FULL_MIN_EMPTY = 41
    MAX_INVENTORY_SIZE = 90
    numItems = MAX_INVENTORY_SIZE
    for i in range(0,MAX_INVENTORY_SIZE):
        curr_id = player.GetItemIndex(i)
        if curr_id != 51001:
            item.SelectItem(curr_id)
            s = item.GetItemSize()
            numItems+=s[0]*s[1]

    if INV_FULL_MIN_EMPTY <= numItems:
        return True
    else:
        return False


def EnergyPacketer():
    if len(listEnergySlot) <= 40:
        shop.ClearPrivateShopStock()
        for x in range(len(listEnergySlot)):
            Log("item ekleniyor")
            if listEnergySlot[x] != 91:
                shop.AddPrivateShopItemStock(1,listEnergySlot[x],x-1,yang-1,0)
        shop.BuildPrivateShop('EnerGia FRAGMENTOS')
    else:
        shop.ClearPrivateShopStock()
        for x in range(41):
            if listEnergySlot[x] != 91:
                Log("item ekleniyor")
                shop.AddPrivateShopItemStock(1,listEnergySlot[x],x-1,yang-1,0)
        shop.BuildPrivateShop('EnerGia FRAGMENTOS')

def HaveAPacket():
    INV_FULL_MIN_EMPTY = 89
    MAX_INVENTORY_SIZE = 90
    numItems = MAX_INVENTORY_SIZE
    for i in range(0,MAX_INVENTORY_SIZE):
        curr_id = player.GetItemIndex(i)
        if curr_id == 50200:
            item.SelectItem(curr_id)
            s = item.GetItemSize()
            numItems-=s[0]*s[1]

    if numItems <= INV_FULL_MIN_EMPTY:
        return True
    else:
        return False

def MainLoop():
    global roadonv1mode
    global energymode
    global rv1clicked
    global needpacket
    global needenergy
    global searchstat
    global pagecheck
    global pagenumber
    global lastcheck
    global priceokey
    global yang
    global minyang
    global bazaarStat
    

    ListOfEnergyFragment()
    if background.GetCurrentMapName() == redVillage1:
        needpacket = 0
        pagecheck = 0
        searchstat = 0
        bazaarStat = 0
        pagenumber = 1
        needenergy = 0
        historysml.moveWaiterTrd4 = 0
        historysml.moveWaiterTrd2 = 0
        historysml.moveWaiterTrd3 = 0
        historysml.moveWaiterTrd1 = 0

    if background.GetCurrentMapName() == redVillage1 and player.GetMoney() >= 100000:
        moneycheck = 1
    
    elif background.GetCurrentMapName() == redVillage1 and player.GetMoney() <= 100000:
        moneycheck = 0


    if background.GetCurrentMapName() == redVillage1 and len(listEnergySlot) << 41 and energymode == 0  and historysml.moveWaiterMap2 == 0 and roadonv1mode == 0 :
        Log("1")
        TimeToGo(WeaponDealerRV1[0],WeaponDealerRV1[1],WeaponDealerRV1[2])
        mx,my,mz = player.GetMainCharacterPosition()
    

    if WeaponDealerRV1[1]-250 <= player.GetMainCharacterPosition()[1] <= WeaponDealerRV1[1]+250 and WeaponDealerRV1[0]-250 <= player.GetMainCharacterPosition()[0] <= WeaponDealerRV1[0]+250 and len(listEnergySlot) << 41 and roadonv1mode == 0 and background.GetCurrentMapName() == redVillage1 :
        historysml.moveWaiterMap2 = 1
        
        Log("2")

    if 1 <= historysml.moveWaiterMap2 <= 26 and energymode == 0 and background.GetCurrentMapName() == redVillage1 and len(listEnergySlot) << 41 and roadonv1mode == 0 :
        player.OnKeyDown(app.DIK_W)
        historysml.moveWaiterMap2 += 1
        Log("3")
        if historysml.moveWaiterMap2 == 25:
            player.OnKeyUp(app.DIK_W)
            player.OnKeyDown(app.DIK_SPACE)
            player.OnKeyUp(app.DIK_SPACE)
            historysml.moveWaiterMap2 = 0
            Log("3-1")
            energymode = 2

    if background.GetCurrentMapName() == redVillage1 and energymode == 2 and len(listEnergySlot) << 41 and roadonv1mode == 0 :
        TimeToGo(WeaponDealerRV1[0],WeaponDealerRV1[1],WeaponDealerRV1[2])
        Log("4")
        if WeaponDealerRV1[1]-250 <= player.GetMainCharacterPosition()[1] <= WeaponDealerRV1[1]+250 and WeaponDealerRV1[0]-250 <= player.GetMainCharacterPosition()[0] <= WeaponDealerRV1[0]+250:
            energymode = 1
            Log("4-1")
    
    if len(listEnergySlot) << 41 and background.GetCurrentMapName() == redVillage1 and roadonv1mode == 0 and energymode == 1 :
        Log("selam")
        EnergyBot()

        if 41 == len(listEnergySlot) or moneycheck == 0:
            energymode = 0
            roadonv1mode = 1
            Log("5-1")
    
    if 1==1 and roadonv1mode == 1 and (len(listEnergySlot) >= 41 or moneycheck == 0)  and background.GetCurrentMapName() == redVillage1 and energymode == 0 and historysml.moveWaiterMap1 == 0:
        
        TimeToGo(tradeAdminCoorRV1[0],tradeAdminCoorRV1[1],tradeAdminCoorRV1[2])

    if tradeAdminCoorRV1[1]-250 <= player.GetMainCharacterPosition()[1] <= tradeAdminCoorRV1[1]+250 and tradeAdminCoorRV1[0]-250 <= player.GetMainCharacterPosition()[0] <= tradeAdminCoorRV1[0]+250 and (len(listEnergySlot) >= 41 or moneycheck == 0) and background.GetCurrentMapName() == redVillage1 and energymode == 0 and roadonv1mode == 1:
        historysml.moveWaiterMap1 = 1
        

    if 1 <= historysml.moveWaiterMap1 <= 46 and roadonv1mode == 1 and background.GetCurrentMapName() == redVillage1 and (len(listEnergySlot) >= 41 or moneycheck == 0) and energymode == 0:
        player.OnKeyDown(app.DIK_W)
        historysml.moveWaiterMap1 += 1
        if historysml.moveWaiterMap1 == 45:
            roadonv1mode = 2
            player.OnKeyUp(app.DIK_W)
            player.OnKeyDown(app.DIK_SPACE)
            player.OnKeyUp(app.DIK_SPACE)
            historysml.moveWaiterMap1 = 1
            roadonv1mode = 2

    if background.GetCurrentMapName() == redVillage1 and roadonv1mode == 2 and (len(listEnergySlot) >= 41 or moneycheck == 0) and energymode == 0:
        TimeToGo(tradeAdminCoorRV1[0],tradeAdminCoorRV1[1],tradeAdminCoorRV1[2])
        if tradeAdminCoorRV1[1]-250 <= player.GetMainCharacterPosition()[1] <= tradeAdminCoorRV1[1]+250 and tradeAdminCoorRV1[0]-250 <= player.GetMainCharacterPosition()[0] <= tradeAdminCoorRV1[0]+250:
            roadonv1mode = 3
            rv1clicked = 0

    if 1 <= historysml.moveWaiterMap1 <= 31 and roadonv1mode == 3 and background.GetCurrentMapName() == redVillage1 and (len(listEnergySlot) >= 41 or moneycheck == 0) and energymode == 0:
        player.OnKeyDown(app.DIK_W)
        historysml.moveWaiterMap1 += 1
        if historysml.moveWaiterMap1 == 30:
            roadonv1mode = 4
            player.OnKeyUp(app.DIK_W)
            player.OnKeyDown(app.DIK_SPACE)
            player.OnKeyUp(app.DIK_SPACE)
            historysml.moveWaiterMap1 = 0
            roadonv1mode = 4

    if background.GetCurrentMapName() == redVillage1 and roadonv1mode == 4 and (len(listEnergySlot) >= 41 or moneycheck == 0) and energymode == 0:
        TimeToGo(tradeAdminCoorRV1[0],tradeAdminCoorRV1[1],tradeAdminCoorRV1[2])
        if tradeAdminCoorRV1[1]-250 <= player.GetMainCharacterPosition()[1] <= tradeAdminCoorRV1[1]+250 and tradeAdminCoorRV1[0]-250 <= player.GetMainCharacterPosition()[0] <= tradeAdminCoorRV1[0]+250:
            roadonv1mode = 5
            rv1clicked = 0

    if roadonv1mode == 5 and background.GetCurrentMapName() == redVillage1 and (len(listEnergySlot) >= 41 or moneycheck == 0) and rv1clicked == 0:
        ClickTheNpc("Trade Administrator")
        event.SelectAnswer(1,1)
        event.SelectAnswer(1,0)
        rv1clicked = 1
        roadonv1mode = 0



    if background.GetCurrentMapName() == tradeMap:
        rv1clicked = 0
        roadonv1mode = 0
        historysml.moveWaiterMap1 = 0
        historysml.moveWaiterMap2 = 0
        energymode = 0
        ListOfEnergyFragment()


    if background.GetCurrentMapName() == tradeMap and HaveAPacket() == False and (needpacket == 1 or needpacket == 0) and player.IsOpenPrivateShop() == 0:
        needpacket = 1

    elif background.GetCurrentMapName() == tradeMap and HaveAPacket() == True and needpacket == 1 or 0 and player.IsOpenPrivateShop() == 0:
        needpacket = 0
    
    if background.GetCurrentMapName() == tradeMap and needpacket == 1 and historysml.moveWaiterTrd1 == 0 and player.IsOpenPrivateShop() == 0:
        TimeToGo(NpcMarketCoorTA[0],NpcMarketCoorTA[1],NpcMarketCoorTA[2])
        

    if background.GetCurrentMapName() == tradeMap and NpcMarketCoorTA[1]-250 <= player.GetMainCharacterPosition()[1] <= NpcMarketCoorTA[1]+250 and NpcMarketCoorTA[0]-250 <= player.GetMainCharacterPosition()[0] <= NpcMarketCoorTA[0]+250 and needpacket == 1 and player.IsOpenPrivateShop() == 0:
        historysml.moveWaiterTrd1 = 1
        needpacket = 2

    if 1 <= historysml.moveWaiterTrd1 <= 31 and   background.GetCurrentMapName() == tradeMap and needpacket == 2 and player.IsOpenPrivateShop() == 0:
        player.OnKeyDown(app.DIK_W)
        historysml.moveWaiterTrd1 += 1
        if historysml.moveWaiterTrd1 == 30:
            needpacket = 3
            player.OnKeyUp(app.DIK_W)
            player.OnKeyDown(app.DIK_SPACE)
            player.OnKeyUp(app.DIK_SPACE)
            historysml.moveWaiterTrd1 = 0

    if background.GetCurrentMapName() == tradeMap and needpacket == 3 and player.IsOpenPrivateShop() == 0:
        TimeToGo(NpcMarketCoorTA[0],NpcMarketCoorTA[1],NpcMarketCoorTA[2])
        if NpcMarketCoorTA[1]-250 <= player.GetMainCharacterPosition()[1] <= NpcMarketCoorTA[1]+250 and NpcMarketCoorTA[0]-250 <= player.GetMainCharacterPosition()[0] <= NpcMarketCoorTA[0]+250:
            needpacket = 4

    if background.GetCurrentMapName() == tradeMap and needpacket == 4 and player.IsOpenPrivateShop() == 0:
        ClickTheNpc("General Store Saleswoman")
        event.SelectAnswer(1,0)
        net.SendShopBuyPacket(23, 0, 1)
        needpacket = 0

    if background.GetCurrentMapName() == tradeMap and len(listEnergySlot) == 1 and (needenergy == 1 or needenergy == 0):
        needenergy = 1

    if len(listEnergySlot) >= 2 and background.GetCurrentMapName() == tradeMap and (needenergy == 1 or needenergy == 0):
        needenergy = 0

    if background.GetCurrentMapName() == tradeMap and len(listEnergySlot) == 1 and player.IsOpenPrivateShop() == 0 and needenergy == 1:
        TimeToGo(tradeAdminCoorTA[0],tradeAdminCoorTA[1],tradeAdminCoorTA[2])
        

    if background.GetCurrentMapName() == tradeMap and player.IsOpenPrivateShop() == 0 and tradeAdminCoorTA[1]-250 <= player.GetMainCharacterPosition()[1] <= tradeAdminCoorTA[1]+250 and tradeAdminCoorTA[0]-250 <= player.GetMainCharacterPosition()[0] <= tradeAdminCoorTA[0]+250 and len(listEnergySlot) == 1 and needenergy == 1:
            historysml.moveWaiterTrd5 = 1
            needenergy = 2

    

    if 1 <= historysml.moveWaiterTrd5 <= 31 and   background.GetCurrentMapName() == tradeMap and needenergy == 2 and player.IsOpenPrivateShop() == 0:
        player.OnKeyDown(app.DIK_W)
        historysml.moveWaiterTrd5 += 1
        if historysml.moveWaiterTrd5 == 30:
            needenergy = 3
            player.OnKeyUp(app.DIK_W)
            player.OnKeyDown(app.DIK_SPACE)
            player.OnKeyUp(app.DIK_SPACE)
            historysml.moveWaiterTrd5 = 0
    
    if background.GetCurrentMapName() == tradeMap and needenergy == 3 and player.IsOpenPrivateShop() == 0:
        TimeToGo(tradeAdminCoorTA[0],tradeAdminCoorTA[1],tradeAdminCoorTA[2])
        if tradeAdminCoorTA[1]-250 <= player.GetMainCharacterPosition()[1] <= tradeAdminCoorTA[1]+250 and tradeAdminCoorTA[0]-250 <= player.GetMainCharacterPosition()[0] <= tradeAdminCoorTA[0]+250:
            needenergy = 4

    if background.GetCurrentMapName() == tradeMap and needenergy == 4 and player.IsOpenPrivateShop() == 0:
        ClickTheNpc("Trade Administrator")
        event.SelectAnswer(0,0)
        event.SelectAnswer(0,0)
        needenergy = 0

    if background.GetCurrentMapName() == tradeMap and needpacket == 0 and len(listEnergySlot) >= 2 and searchstat == 0 and player.IsOpenPrivateShop() == 0:
        TimeToGo(SellAreaCoor[0],SellAreaCoor[1],SellAreaCoor[2])
        

    if background.GetCurrentMapName() == tradeMap and SellAreaCoor[1]-250 <= player.GetMainCharacterPosition()[1] <= SellAreaCoor[1]+250 and SellAreaCoor[0]-250 <= player.GetMainCharacterPosition()[0] <= SellAreaCoor[0]+250 and needpacket == 0 and len(listEnergySlot) >= 2 and historysml.moveWaiterTrd2 == 0 and searchstat == 0 and len(listEnergySlot) >= 2 and player.IsOpenPrivateShop() == 0:
        net.SendPrivateShopSearchInfoByVnum(51001,0,100000000,0,999,0)
        Log("Item araniyor")
        historysml.moveWaiterTrd2 = 1

    if 1 <= historysml.moveWaiterTrd2 <= 25 and background.GetCurrentMapName() == tradeMap and searchstat == 0 and len(listEnergySlot) >= 2 and player.IsOpenPrivateShop() == 0:
        Log("Bekleniyor")
        historysml.moveWaiterTrd2 += 1
    if 25 <= historysml.moveWaiterTrd2 <=27 and background.GetCurrentMapName() == tradeMap and searchstat == 0 and len(listEnergySlot) >= 2 and player.IsOpenPrivateShop() == 0:
        Log(historysml.moveWaiterTrd3)
        pagecheck = 1
        
        
        
        if historysml.moveWaiterTrd3 == 0 and searchstat == 0:
            net.SendPrivateShopSearchInfoSub(pagenumber)
        
        historysml.moveWaiterTrd3 += 1

        if 1 <= historysml.moveWaiterTrd3 <= 60 and pagecheck ==1 and searchstat == 0:
            Log("littlewait")
            historysml.moveWaiterTrd3 += 1

        if historysml.moveWaiterTrd3 == 62 and searchstat == 0:
            if (shop.GetPrivateShopSearchResult(0)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(0)[3]
                Log("1.")   
                    
                    
                if lastcheck <= minyang:
                    yang = minyang
                    historysml.moveWaiterTrd2 = 28
                    historysml.moveWaiterTrd3 = 0

                else:
                    yang = lastcheck
                    historysml.moveWaiterTrd2 = 28
                    historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(1)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(1)[3]
                Log("2.") 
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(2)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(2)[3]
                Log("3.")             
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(3)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(3)[3]
                Log("4.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(4)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(4)[3]
                Log("5.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(5)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(5)[3]
                Log("6.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(6)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(6)[3]
                Log("7.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(7)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(7)[3]
                Log("8.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(8)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(8)[3]
                Log("9.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            elif (shop.GetPrivateShopSearchResult(9)[2] == 200 and priceokey == 0) and searchstat == 0:
                lastcheck = shop.GetPrivateShopSearchResult(9)[3]
                Log("10.") 
                        
                        
                if lastcheck <= minyang:
                        yang = minyang
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

                else:
                        yang = lastcheck
                        historysml.moveWaiterTrd2 = 28
                        historysml.moveWaiterTrd3 = 0

            else:
                Log("Sayfa degisiyor.") 
                pagenumber += 1
                historysml.moveWaiterTrd3= 0

    if 1==1 and historysml.moveWaiterTrd2 == 28 and searchstat == 0  and len(listEnergySlot) >= 2 and player.IsOpenPrivateShop() == 0:
        Log("Fiyat kontrolu Bitti")
        Log("En ucuzu:")
        Log(yang)
        searchstat = 1
        historysml.moveWaiterTrd2 = 0


    if player.IsOpenPrivateShop() == 0 and len(listEnergySlot) >= 2 and background.GetCurrentMapName() == tradeMap  and searchstat == 1 and bazaarStat == 0 :
        
        Log("Basardim")
        EnergyPacketer()
        bazaarStat = 1
            

    if player.IsOpenPrivateShop() == 1 and background.GetCurrentMapName() == tradeMap :
        if len(listEnergySlot) >= 2 and historysml.moveWaiterTrd4 <= 2499:
            historysml.moveWaiterTrd4 += 1
            Log(historysml.moveWaiterTrd4)
        elif len(listEnergySlot) >= 2 and historysml.moveWaiterTrd4 == 2500:
            searchstat = 0
            bazaarStat = 0
            historysml.moveWaiterTrd4 = 0
            historysml.moveWaiterTrd2 = 0
            pagenumber = 1
            net.SendPrivateShopClose()
        elif len(listEnergySlot) == 1:
            net.SendPrivateShopClose()
            searchstat = 0
            bazaarStat = 0
            historysml.moveWaiterTrd4 = 0
            historysml.moveWaiterTrd2 = 0
            pagenumber = 1

    if GetCurrentPhase() != 5:
        energymode = 0
        roadonv1mode = 0
        clicked = 0
        timerweapondelar = 0
        waitontrd = 0
        sellmode = 0
        debugtime= 0
        steppedcount = 0
        rv1clicked = 0
        moveWaiterMap1Energy = 0
        moveWaiterMap1Trade = 0
        moneycheck = 0
        needpacket = 0
        pagecheck = 0
        needenergy = 0
        searchstat = 0
        pagenumber = 1
        priceokey = 0
        bazaarStat = 0
        historysml.moveWaiterMap1 = 0
        historysml.moveWaiterMap2 = 0
        historysml.moveWaiterTrd1 = 0
        historysml.moveWaiterTrd2 = 0
        historysml.moveWaiterTrd3 = 0
        historysml.moveWaiterTrd4 = 0
        historysml.moveWaiterTrd5 = 0

phaseCallbacks = {}
CURRENT_PHASE = 5

def phaseIntercept(*args,**kwargs):
	#printFuncNC(*args,**kwargs)
	global CURRENT_PHASE
	if len(args)>1 and args[1] != 0:
		CURRENT_PHASE = args[0]
	
	for callback_id in phaseCallbacks:
		callback = phaseCallbacks[callback_id]
		if callable(callback):
			callback(CURRENT_PHASE,args[1])
	phaseHook.CallOriginalFunction(*args,**kwargs)

phaseHook = Hook(net.SetPhaseWindow,phaseIntercept)
phaseHook.HookFunction()


def GetCurrentPhase():
	global CURRENT_PHASE
	return CURRENT_PHASE
        

    

    

    




                        
            



        
               

                    
                    
            

