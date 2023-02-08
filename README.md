You need to have Keep-Crafting for this script. (https://github.com/swkeep/keep-crafting) 

Replace this in Keep-Crafting -> client -> client_lib -> menu.lua:
RegisterKeyMapping('+crafting_menu', 'crafting_menu', 'keyboard', 'e')
RegisterCommand('+crafting_menu', function()
     local state, workbench = GetClosest_Workbenches()
     if not IsPauseMenuActive() and state then
          Workbench = workbench
          menu:main_categories()
          return
     end
end, false)

With this:
RegisterKeyMapping('+crafting_menu', 'crafting_menu', 'keyboard', 'e')
RegisterCommand('+crafting_menu', function()
     local state, workbench = GetClosest_Workbenches()
     if not IsPauseMenuActive() and state then
          Workbench = workbench
          if workbench.type == "weapon" then
               local citizenid = QBCore.Functions.GetPlayerData().citizenid
               QBCore.Functions.TriggerCallback("ROVELT_mission:server:getqueset",function(info)
                    
                    if info == "0" then
                         QBCore.Functions.Notify("Don't know how to use this?", "error")
                    else
                         menu:main_categories()
                    end
               end,citizenid) 
          else
               menu:main_categories()
          end
          return
     end
end, false)

Put this in Keep-Crafting -> Config.lua (Under Config.categories):

     ['pistol'] = {
          key = 'pistol',
          label = 'Pistol Bench',
          icon = 'fa-solid fa-gun',
          jobs = {},
          sub_categories = {
               ['pistol'] = {
                    icon = 'fa-solid fa-gun',
                    label = 'Pistol',
               },
               ['smg'] = {
                    icon = 'fa-solid fa-gun',
                    label = 'smg',
               },
               ['shotgun'] = {
                    icon = 'fa-solid fa-gun',
                    label = 'shotgun',
               },
               ['attachments'] = {
                    icon = 'fa-solid fa-gun',
                    label = 'Attachments',
               },
          }
     },

Put this in Keep-Crafting -> Config.lua (Under Config.workbenches)
     {
          table_model = 'gr_prop_gr_bench_02b',
          coords = vector3(-722.3, 5773.49, 17.05),
          item_show_case_offset = vector3(0.0, 0.0, 1.2),
          rotation = vector3(0.0, 0.0, 110.53),
          job = {
               allowed_list = {},
               allowed_grades = {}
          },
          categories = { Config.categories.Weapon },
          recipes = { weapon_recipe },
          type = "weapon",
          radius = 3.0
     },


Put this in Keep-Crafting -> Config.lua (Just somewhere):
local weapon_recipe = {
     
     ['pistol_ammo'] = {
          categories = {
               sub = 'pistol',
          },
          item_settings = {
               label = 'Pistol Ammo',
               image = 'pistol_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 12,
               materials = {
                    ["iron"] = 10,
                    ["steel"] = 10,
                    ["copper"] = 15,
                    ["metalscrap"] = 15,
               },
               exp_per_craft = 5
          }
     },
     ['pistol_ammo2'] = {
          categories = {
               sub = 'pistol',
          },
          item_settings = {
               label = 'Pistol Ammo 10x',
               image = 'pistol_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 10, -- crafted amount
               duration = 120,
               materials = {
                    ["iron"] = 100,
                    ["steel"] = 100,
                    ["copper"] = 150,
                    ["metalscrap"] = 150,
               },
               exp_per_craft = 50
          }
     },
     ['weapon_pistol'] = {
          categories = {
               sub = 'pistol',
          },
          item_settings = {
               label = 'Pistol',
               image = 'weapon_pistol', -- use inventory's images
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 250,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 20,
               materials = {
                    ["aluminum"] = 80,
                    ["steel"] = 50,
                    ["rubber"] = 30,
                    ["pistoldel"] = 10,
               },
               exp_per_craft = 5
          }
     },
     ['pistol_extendedclip'] = {
          categories = {
               sub = 'attachments',
          },
          item_settings = {
               label = 'Pistol Extended Clip',
               image = 'pistol_extendedclip', -- use inventory's images pistol50_extendedclip
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 750,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["copper"] = 50,
                    ["aluminum"] = 25,
                    ["rubber"] = 25,
                    ["metalscrap"] = 50,
               },
               exp_per_craft = 5
          }
     },
     ['weapon_pistol50'] = {
          categories = {
               sub = 'pistol',
          },
          item_settings = {
               label = 'Pistol 50',
               image = 'weapon_pistol50', -- use inventory's images pistol50_extendedclip
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 550,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["storpistoldel"] = 10,
                    ["steel"] = 70,
                    ["metalscrap"] = 50,
               },
               exp_per_craft = 5
          }
     },
     ['pistol50_extendedclip'] = {
          categories = {
               sub = 'attachments',
          },
          item_settings = {
               label = 'Pistol 50 Extended clip',
               image = 'pistol50_extendedclip', -- use inventory's images pistol50_extendedclip
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 750,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["copper"] = 50,
                    ["aluminum"] = 25,
                    ["rubber"] = 25,
                    ["metalscrap"] = 50,
               },
               exp_per_craft = 5
          }
     },
     ['weapon_snspistol'] = {
          categories = {
               sub = 'pistol',
          },
          item_settings = {
               label = 'Pistol',
               image = 'weapon_snspistol', -- use inventory's images
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 250,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 20,
               materials = {
                    ["aluminum"] = 80,
                    ["steel"] = 50,
                    ["rubber"] = 30,
                    ["lilledel"] = 10,
               },
               exp_per_craft = 5
          }
     },
     ['smg_ammo'] = {
          categories = {
               sub = 'smg',
          },
          item_settings = {
               label = 'SMG Ammo',
               image = 'smg_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 15,
               materials = {
                    ["aluminum"] = 15,
                    ["steel"] = 15,
                    ["rubber"] = 20,
                    ["metalscrap"] = 5,
                    ["copper"] = 15,
               },
               exp_per_craft = 5
          }
     },
     ['smg_ammo2'] = {
          categories = {
               sub = 'smg',
          },
          item_settings = {
               label = 'SMG Ammo 10x',
               image = 'smg_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 10, -- crafted amount
               duration = 150,
               materials = {
                    ["aluminum"] = 150,
                    ["steel"] = 150,
                    ["rubber"] = 200,
                    ["metalscrap"] = 50,
                    ["copper"] = 150,
               },
               exp_per_craft = 50
          }
     },
     ['weapon_machinepistol'] = {
          categories = {
               sub = 'smg',
          },
          item_settings = {
               label = 'Machinepistol',
               image = 'weapon_machinepistol', -- use inventory's images
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 1250,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["aluminum"] = 80,
                    ["steel"] = 70,
                    ["rubber"] = 30,
                    ["smgdel"] = 10,
               },
               exp_per_craft = 5
          }
     },
     ['weapon_microsmg'] = {
          categories = {
               sub = 'smg',
          },
          item_settings = {
               label = 'Microsmg',
               image = 'weapon_microsmg', -- use inventory's images
               object = {
                    name = 'w_sb_smgmk2_mag2',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 1550,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["smgdel"] = 15,
                    ["steel"] = 90,
                    ["metalscrap"] = 50,
                    ["copper"] = 150,
               },
               exp_per_craft = 5
          }
     },
     ['shotgun_ammo'] = {
          categories = {
               sub = 'shotgun',
          },
          item_settings = {
               label = 'Shotgun Ammo',
               image = 'shotgun_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 20,
               materials = {
                    ["aluminum"] = 15,
                    ["steel"] = 15,
                    ["rubber"] = 20,
                    ["metalscrap"] = 25,
                    ["copper"] = 150,
               },
               exp_per_craft = 5
          }
     },
     ['shotgun_ammo2'] = {
          categories = {
               sub = 'shotgun',
          },
          item_settings = {
               label = 'Shotgun Ammo 10x',
               image = 'shotgun_ammo', -- use inventory's images
               object = {
                    name = 'prop_ld_ammo_pack_01',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 150,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 10, -- crafted amount
               duration = 200,
               materials = {
                    ["aluminum"] = 150,
                    ["steel"] = 150,
                    ["rubber"] = 200,
                    ["metalscrap"] = 250,
                    ["copper"] = 150,
               },
               exp_per_craft = 50
          }
     },
     ['weapon_dbshotgun'] = {
          categories = {
               sub = 'shotgun',
          },
          item_settings = {
               label = 'DB Shotgun',
               image = 'weapon_dbshotgun', -- use inventory's images
               object = {
                    name = 'w_pi_pistol50',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 1250,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["aluminum"] = 80,
                    ["steel"] = 70,
                    ["rubber"] = 30,
                    ["shotgundel"] = 10,
               },
               exp_per_craft = 5
          }
     },
     ['weapon_sawnoffshotgun'] = {
          categories = {
               sub = 'shotgun',
          },
          item_settings = {
               label = 'Sawnoff shotgun',
               image = 'weapon_sawnoffshotgun', -- use inventory's images
               object = {
                    name = 'w_sb_smgmk2_mag2',
                    rotation = vector3(45.0, 0.0, 0.0)
               },
               level = 2550,
               job = {
                    allowed_list = {},
                    allowed_grades = {}
               }
          },
          crafting = {
               show_level_in_mail = true,
               success_rate = 100,
               amount = 1, -- crafted amount
               duration = 60,
               materials = {
                    ["shotgundel"] = 15,
                    ["steel"] = 90,
                    ["metalscrap"] = 50,
                    ["copper"] = 150,
               },
               exp_per_craft = 5
          }
     },
}
