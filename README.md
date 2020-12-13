# HOI4-Colonization-mechanic
This is a simple colonization mechanic made with scripted GUI for HOI4, feel free to use it in your mod or use code from it if given credit.

P.S Interface is not included, the current interface is very poorly made, only containing 2 buttons, a progressbar and a variable

# How it works ?
This is mechanic is made using arrays, progressbars and variables, pressing the colonize button will add the current selected state to the array and set a state_flag for that state, after adding the state to the array using the for_each_scope_loob scope, it adds the value 1 every day using on_actions to the current variable until the specified value is reached. After the specified value is reached the selected state gets transfered to the current country using ROOT = { transfer_state = PREV }.

https://streamable.com/iktut7

# How can i add it in my mod ?
Simply download the files and paste each file into the corresponding folder.

# How can i set which country can be colonized, when can it be colonized and who can colonize it ?
You can set which country can colonize by simply changing the TAGS to which countries you want to colonize, for example now the countries that can colonize are NAV,SPR,TUR,GLC,SOV,FIN,NOR,SWE,ITA,MEX and POR, you can remove the whole 

			`ROOT  ={
				OR ={
					tag = NAV
					tag = SPR
					tag = TUR
					tag = GLC
					tag = SOV
					tag = FIN
					tag = NOR
					tag = SWE
					tag = ITA
					tag = MEX
					tag = POR
				}
			}`
		
 if you want every country to be able to colonize
    
   If you want to change which country can be colonized change FRA to which country you want to be colonized from the is_fully_controlled_by = FRA line of code. If you want more countries to be colonized just put the line of code in the OR = { } scope, for example :
   `OR = {
    is_fully_controlled_by = FRA
    is_fully_controlled_by = ITA
   }`
    
  If you want to chage in what circumstances someone can colonize change this line of code, 		
		`visible = {
			ROOT  ={
				OR ={
					tag = NAV
					tag = SPR
					tag = TUR
					tag = GLC
					tag = SOV
					tag = FIN
					tag = NOR
					tag = SWE
					tag = ITA
					tag = MEX
					tag = POR
				}
			}
			AND = {
				is_fully_controlled_by = FRA
				FROM = {
					OR={
						any_country = {
							AND = {
								is_subject_of = ROOT
								any_owned_state = {
									any_neighbor_state = {
										state = PREV.PREV.PREV

									}
								}
							}
						}
						any_neighbor_state = { is_owned_by = ROOT }
					}
				}
			}
			
		}`
		
`Now beacuse I don't know how would you want to be able to colonize I'm gonna give a example and hope that you can understand how I do it and copy it.
    
    visible = {
			ROOT  ={
				has_idea = colonization_idea
				has_country_flag = colonization_flag
				OR ={
					tag = NAV
					tag = SPR
					tag = TUR
					tag = GLC
					tag = SOV
					tag = FIN
					tag = NOR
					tag = SWE
					tag = ITA
					tag = MEX
					tag = POR
				}
			}
			AND = {
				is_fully_controlled_by = FRA
				FROM = {
					OR={
						any_country = {
							AND = {
								is_subject_of = ROOT
								any_owned_state = {
									any_neighbor_state = {
										state = PREV.PREV.PREV

									}
								}
							}
						}
						any_neighbor_state = { is_owned_by = ROOT }
					}
				}
			}
			
		}
    
 In this example I made it so you are able to colonize if the ROOT ( the country) has the `idea colonization_idea` and the `colonization_flag` flag
		
	
