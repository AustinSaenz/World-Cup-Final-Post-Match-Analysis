# 2022 World Cup Final | Post-Match Analysis

This project analyzes the match statistics for the entire match between Argentina and France during the 2022 World Cup final. The goal of this project was to enhance my EDA skills by examining almost every match statistic within this instant classic. My analysis includes six main graphs created using Python within Jupyter Notebooks, as well as several other findings which contributed to creating said graphs. Below you'll find the graphs associated with my main post-match analysis, but feel free to explore my [Full Code](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/2022%20FIFA%20World%20Cup%20Final%20Analysis.ipynb) if you want every analysis!


## Table of Contents


1. [Starting XI Formation Pitch Graphic](#1-starting-xi-formation-pitch-graphic)
2. [Argentina vs France: Match Statistics](#2-argentina-vs-france-match-statistics)
3. [Argentina 4-3-3 Passing Map](#3-argentina-4-3-3-passing-map)
4. [France 4-2-3-1 Passing Map](#4-france-4-2-3-1-passing-map)
5. [Argentina vs France: Shot Map](#5-argentina-vs-france-shot-map)
6. [Argentina vs France: Possession Chart](#6-argentina-vs-france-possession-chart)
7. [Full Code](#7-full-code)

## 1. Starting XI Formation Pitch Graphic

This graph displays the starting XI formation pitch graphic for both teams.


```python
# Both Teams Starting XI Formation
france_formation = france_starting_XI['formation'].iloc[0]
argentina_formation = argentina_starting_XI['formation'].iloc[0]

# Convert formation to a string if it's not already
france_formation = str(france_formation)
argentina_formation = str(argentina_formation)

# Replace France's player names with the shorter version
france_player_short_names = {'Hugo Lloris': 'Hugo Lloris(C)',
                      'Jules Koundé': 'Jules Koundé',
                      'Raphaël Varane': 'Raphaël Varane',
                      'Dayotchanculle Upamecano': 'Dayot Upamecano',
                      'Theo Bernard François Hernández': 'Theo Hernández',
                      'Aurélien Djani Tchouaméni': 'Aurélien Tchouaméni',
                      'Adrien Rabiot': 'Adrien Rabiot',
                      'Ousmane Dembélé': 'Ousmane Dembélé',
                      'Antoine Griezmann': 'Antoine Griezmann',
                      'Kylian Mbappé Lottin': 'Kylian Mbappé',
                      "Olivier Giroud": "Olivier Giroud"}
france_starting_XI['player_name'] = france_starting_XI['player_name'].replace(france_player_short_names)

# Replace Argentina's player names with the shorter version
argentina_player_short_names = {'Damián Emiliano Martínez': 'Emiliano Martínez',
                      'Nahuel Molina Lucero': 'Nahuel Molina',
                      'Cristian Gabriel Romero': 'Cristian Romero',
                      'Nicolás Hernán Otamendi': 'Nicolás Otamendi',
                      'Nicolás Alejandro Tagliafico': 'Nicolás Tagliafico',
                      'Enzo Fernandez': 'Enzo Fernandez',
                      'Rodrigo Javier De Paul': 'Rodrigo De Paul',
                      'Alexis Mac Allister': 'Alexis Mac Allister',
                      'Lionel Andrés Messi Cuccittini': 'Lionel Messi (C)',
                      'Ángel Fabián Di María Hernández': 'Ángel Di María',
                      "Julián Álvarez": "Julián Álvarez"}
argentina_starting_XI['player_name'] = argentina_starting_XI['player_name'].replace(argentina_player_short_names)

pitch = VerticalPitch(goal_type='box', pitch_color='#3e7d1b', line_color='white', stripe_color='#4c8527', stripe=True)
fig, ax = pitch.draw(figsize=(14, 14))

# Plot France's starting formation on one half of the field
ax_text_france = pitch.formation(france_formation, positions=france_starting_XI.position_id, kind='text',
                                  text=france_starting_XI.player_name.str.replace(' ', '\n'),xoffset=3,
                                  va='center', ha='center', fontsize=14, ax=ax, half=True)

ax_scatter_france = pitch.formation(france_formation, positions=france_starting_XI.position_id, kind='scatter',
                                     c='#21304D', hatch='_', linewidth=5, s=1000, half=True,
                                     xoffset=-2, ax=ax, edgecolor='#ED2939')

# Plot Argentina's starting formation on the other half of the field
ax_text_argentina = pitch.formation(argentina_formation, positions=argentina_starting_XI.position_id, kind='text',
                                    text=argentina_starting_XI.player_name.str.replace(' ', '\n'), xoffset=-3,
                                    va='center', ha='center', fontsize=14, ax=ax, half=True, flip=True)

ax_scatter_argentina = pitch.formation(argentina_formation, positions=argentina_starting_XI.position_id, kind='scatter',
                                       c='#43A1D5', hatch='_', linewidth=5, s=1000, half=True, flip=True,
                                       xoffset=3, ax=ax, edgecolor='#D5B048')

# add title
title = "Argentina vs France\n2022 FIFA World Cup Final | Starting XI Formations"
ax.set_title(title, fontsize=16, fontweight='bold')

# Add title to the top half (Argentina)
top_left_half_title = "Argentina"
ax.text(0.15, 0.95, top_left_half_title, fontsize=19, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)

top_right_half_title = "4-3-3"
ax.text(0.87, 0.95, top_right_half_title, fontsize=20, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)

argentina_substitutes_title = "Substitutes"
ax.text(1.25, 0.97, argentina_substitutes_title, fontsize=12.5, va='center', ha='center', fontweight='bold',
        color="#43A1D5",transform=ax.transAxes)

# List of Argentina substitute player names
argentina_substitutes = [
    "Franco Armani  GK",
    "Geronimo Rulli  GK",
    "Juan Foyth  DF",
    "Gonzalo Montiel  DF",
    "Leandro Paredes  MF",
    "German Pezzella  DF",
    "Marcos Acuna  MF",
    "Exequiel Palacios  MF",
    "Angel Correa  FW",
    "Thiago Almada  MF",
    "Alejandro Gomez  MF",
    "Guido Rodriguez  MF",
    "Paulo Dybala  FW",
    "Lautaro Martinez  FW",
    "Lisandro Martinez  DF"
]

# Position for the first substitute
x_coordinate = 1.33
y_coordinate = 0.94

# Spacing between player names
line_height = 0.02

# Add the Argentina substitute player names
for substitute in argentina_substitutes:
    ax.text(x_coordinate, y_coordinate, substitute, fontsize=10, va='center', ha='right', color="#43A1D5", transform=ax.transAxes)
    y_coordinate -= line_height


# Add title to the bottom half (France)
bottom_left_half_title = "France"
ax.text(0.12, 0.05, bottom_left_half_title, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#21304D" ,transform=ax.transAxes)

bottom_right_half_title = "4-2-3-1"
ax.text(0.87, 0.05, bottom_right_half_title, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)

# French substitutes title
france_substitutes_title = "Substitutes"
ax.text(1.25, 0.33, france_substitutes_title, fontsize=12.5, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)

# List of French substitute player names
france_substitutes = [
    "Steve Mandanda  GK",
    "Alphonse Areola  GK",
    "Benjamin Pavard  DF",
    "Axel Disasi  DF",
    "Matteo Guendouzi  MF",
    "Randal Kolo Muani  FW",
    "Youssouf Fofana  DF",
    "Jordan Veretout  MF",
    "William Saliba  DF",
    "Karim Benzema  FW",
    "Kingsley Coman  FW",
    "Lucas Hernandez  DF",
    "Ibrahima Konate  DF",
    "Eduardo Camavinga  MF",
    "Marcus Thuram  FW"
    # Add more substitute player names here
]

# Position for the first substitute
x_coordinate = 1.33
y_coordinate = 0.30

# Spacing between player names
line_height = 0.02

# Add the French substitute player names
for substitute in france_substitutes:
    ax.text(x_coordinate, y_coordinate, substitute, fontsize=10, va='center', ha='right', color="#21304D", transform=ax.transAxes)
    y_coordinate -= line_height
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/Starting%20XI%20Formations.png)

## 2. Argentina vs France: Match Statistics

This graph presents overall match statistics between Argentina and France in regulation during the first four periods, excluding the fifth period penalty shootout.


```python
# Let's visualize both teams events

import matplotlib.pyplot as plt
!pip install highlight_text
from highlight_text import fig_text

from mplsoccer import PyPizza, FontManager, add_image
from urllib.request import urlopen
from PIL import Image


# Let's customize the chart and add an image...(Image of WC Trophy)
image_path = r"C:\Anaconda\PROJECTS\2022 FIFA WC Final Analysis\WC_Trophy for Pizza Chart2.jpg"
WC_Trophy = Image.open(image_path)



# Now let's create our comparison chart of event data for each team


# parameter and values list
# The values are taken from the excellent fbref website (supplied by StatsBomb)
params = [
    "Completed Passes", "Possession %", "Fouls Committed",
    "Total Shots", "Expected Goals (xG)",
    "Interceptions", "Total Carries", "Clearances",
    "Count of\nDefensive Pressures", "Tackles",
    "Count of\nDefense Dribbled Past", "Saves"
]
values = [546, 56, 29, 20, 2.8, 13, 527, 26, 167, 26, 22, 3]    # for Argentina National Team
values_2 = [420, 44, 19, 10, 2.3, 15, 413, 19, 194, 31, 9, 7]  # for France National Team


# minimum range value and maximum range value for parameters
min_range = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
max_range = [546, 56, 48, 30, 3, 20, 800, 47, 210, 40, 25, 10]


# instantiate PyPizza class
baker = PyPizza(
    params=params,                  # list of parameters
    min_range=min_range,            # min range values
    max_range=max_range,            # max range values
    background_color="#EBEBE9",     # background color
    straight_line_color="#222222",  # color for straight lines
    straight_line_lw=1,             # linewidth for straight lines
    last_circle_lw=1,               # linewidth of last circle
    last_circle_color="#222222",    # color of last circle
    other_circle_ls="-.",           # linestyle for other circles
    other_circle_lw=1               # linewidth for other circles
)

# plot pizza
fig, ax = baker.make_pizza(
    values,                     # list of values
    compare_values=values_2,    # comparison values
    figsize=(10, 10),             # adjust figsize according to your need
    kwargs_slices=dict(
        facecolor="#43A1D5", edgecolor="#222222", 
        zorder=2, linewidth=1
    ),                          # values to be used when plotting slices
    kwargs_compare=dict(
        facecolor="#21304D", edgecolor="#222222", 
        zorder=2, linewidth=1,
    ),
    kwargs_params=dict(
        color="#000000", fontsize=12, 
        va="center"
    ),                          # values to be used when adding parameter
    kwargs_values=dict(
        color="#000000", fontsize=12, 
      zorder=3,
        bbox=dict(
            edgecolor="#000000", facecolor="#D5B048",
            boxstyle="round,pad=0.2", lw=1
        )
    ),                          # values to be used when adding parameter-values labels
    kwargs_compare_values=dict(
        color="#000000", fontsize=12,  zorder=3,
        bbox=dict(edgecolor="#000000", facecolor="#ED2939", boxstyle="round,pad=0.2", lw=1)
    ),                          # values to be used when adding parameter-values labels
)

# add title
fig_text(
    0.515, 0.99, "<Argentina> vs <France>", size=17, fig=fig,
    highlight_textprops=[{"color": '#43A1D5', "weight": "bold"}, {"color": '#21304D', "weight": "bold"}],
    ha="center", color="#000000"
)


# add subtitle
fig.text(
    0.515, 0.942,
    "2022 FIFA World Cup Final | Post-Match Analysis",
    size=15,
    ha="center",  color="#000000", weight="bold"
)

# add image
ax_image = add_image(
    WC_Trophy, fig, left=0.4478, bottom=0.4315, width=0.13, height=0.127
)
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/Match%20Statistics.png)

## 3. Argentina 4-3-3 Passing Map

This passing map showcases the passing patterns for Argentina throughout the entirety of the match in their 4-3-3 formation.


```python
# NOW LETS CREATE THE PITCH AND PLOT OUR PASSING MAP
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.colors import to_rgba

# NOW LETS MAKE THE NODES BASED OFF POSITION AND NOT PLAYERS 
arg_average_locations = merged_df.groupby('position_abbreviation').agg(
    {'starting_x':['mean'], 'starting_y':['mean', 'count']})
arg_average_locations.columns = ['starting_x', 'starting_y', 'count']
arg_average_locations

# Rename the 'count' column to avoid naming conflict
arg_pass_between.rename(columns={'count': 'counts'}, inplace=True)

#Calculate the line width and marker sizes relative to the largest counts
MAX_LINE_WIDTH = 18
MAX_MARKER_SIZE = 3000
arg_pass_between['width'] = (arg_pass_between.counts / arg_pass_between.counts.max() *
                           MAX_LINE_WIDTH)
arg_average_locations['marker_size'] = (arg_average_locations['count']
                                         / arg_average_locations['count'].max() * MAX_MARKER_SIZE)

#Set the color and transparency of lines when fewer passes are made
MIN_TRANSPARENCY = 0
color = np.array(to_rgba('white'))
color = np.tile(color, (len(arg_pass_between), 1))
c_transparency = arg_pass_between.pass_count / arg_pass_between.pass_count.max()
c_transparency = (c_transparency * (1 - MIN_TRANSPARENCY)) + MIN_TRANSPARENCY
color[:, 3] = c_transparency

# Setup the pitch
pitch = Pitch(pitch_type='statsbomb',pitch_color='#3e7d1b', line_color='white', stripe_color='#4c8527', stripe=True)
fig, ax = pitch.draw(figsize=(16, 10), constrained_layout=False, tight_layout=False)


# Creating the passing arrows
# Calculate the adjustment factor for arrow length
ARROW_LENGTH_FACTOR = 0.9  # Adjust this factor to control arrow length

# Creating the passing arrows with adjusted transparency and length
adjusted_end_x = arg_pass_between.starting_x + (arg_pass_between.starting_x_end - arg_pass_between.starting_x) * ARROW_LENGTH_FACTOR
adjusted_end_y = arg_pass_between.starting_y + (arg_pass_between.starting_y_end - arg_pass_between.starting_y) * ARROW_LENGTH_FACTOR

arg_pass_arrows = pitch.arrows(arg_pass_between.starting_x, arg_pass_between.starting_y, 
                               adjusted_end_x, adjusted_end_y, 
                               lw=arg_pass_between.width, color='#FFFFFF', alpha=c_transparency, zorder=1, ax=ax)

#creating the nodes
arg_pass_nodes = pitch.scatter(arg_average_locations.starting_x, arg_average_locations.starting_y, 
                              s=arg_average_locations.marker_size,
                              color='#D5B048', edgecolors='black', linewidth=0.5, alpha=1, ax=ax)
#creating the internal nodes
arg_pass_nodes_interal = pitch.scatter(arg_average_locations.starting_x, arg_average_locations.starting_y,
                              s=arg_average_locations.marker_size / 2, color = '#43A1D5', edgecolors='black',
                                       linewidth=0.5, alpha=1, ax=ax)


# Add position abbreviations as text labels inside the nodes
for index, row in arg_average_locations.iterrows():
    ax.text(row['starting_x'], row['starting_y'], row.name, color='white',
            fontsize=15, ha='center', va='center', fontweight='bold')

    
# add title
fig_text(
    0.515, 0.99, "Argentina 4-3-3 Passing Map", size=35, fig=fig,
    color='#43A1D5',
    ha="center", weight="bold"
)

# add subtitle
fig.text(
    0.515, 0.915,
    "2022 FIFA World Cup Final | Post-Match Analysis",
    size=20,
    ha="center",  color="#D5B048", weight="bold"
)

# Adding player names and their position played
argentina_player_title = "Players"
ax.text(1.15, .95, argentina_player_title, fontsize=15, va='center', ha='left', fontweight='bold',
        color="#43A1D5",transform=ax.transAxes)

# List of Argentina player names
argentina_players = [
    'Emiliano Martínez',
    'Nahuel Molina / Gonzalo Montiel',
    'Cristian Romero',
    'Nicolás Otamendi',
    'Nicolás Tagliafico / Paulo Dybala',
    'Enzo Fernandez',
    'Rodrigo De Paul/Leandro Paredes',
    'Alexis Mac Allister / German Pezzella',
    'Lionel Messi (C)',
    'Ángel Di María / Marcos Acuna',
    "Julián Álvarez / Lautaro Martínez"
]

# Position for the first substitute
x_coordinate = 1.15
y_coordinate = 0.90

# Spacing between player names
line_height = 0.04

# Add the Argentina substitute player names
for players in argentina_players:
    ax.text(x_coordinate, y_coordinate, players, fontsize=15, va='center', ha='left', color="#43A1D5", transform=ax.transAxes)
    y_coordinate -= line_height
    
#Positions
argentina_pos_title = "Pos."
ax.text(1.05, .95, argentina_pos_title, fontsize=15, va='center', ha='left', fontweight='bold',
        color="#43A1D5",transform=ax.transAxes)

# List of Argentina Positions
argentina_pos = [
    'GK',
    'RB',
    'RCB',
    'LCB',
    'LB',
    'CDM',
    'RCM',
    'LCM',
    'RW',
    'LW',
    "CF",
]

# Position for the first position
pos_x_coordinate = 1.05
pos_y_coordinate = 0.90

# Spacing between player names
pos_line_height = 0.04

# Add the Argentina positions names
for pos in argentina_pos:
    ax.text(pos_x_coordinate, pos_y_coordinate, pos, fontsize=15, va='center', ha='left', color="#43A1D5", transform=ax.transAxes)
    pos_y_coordinate -= pos_line_height
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/Argentina%20Passing%20Map.png)

## 4. France 4-2-3-1 Passing Map

This passing map showcases the passing patterns for France throughout the entirety of the match in their 4-2-3-1 formation.


```python
# NOW LETS CREATE THE PITCH AND PLOT OUR PASSING MAP FOR FRANCE
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.colors import to_rgba

# NOW LETS MAKE THE NODES BASED OFF POSITION AND NOT PLAYERS 
fra_average_locations = fra_merged_df.groupby('position_abbreviation').agg(
    {'starting_x':['mean'], 'starting_y':['mean', 'count']})
fra_average_locations.columns = ['starting_x', 'starting_y', 'count']
fra_average_locations


# Rename the 'count' column to avoid naming conflict
fra_pass_between.rename(columns={'count': 'counts'}, inplace=True)

#Calculate the line width and marker sizes relative to the largest counts
MAX_LINE_WIDTH = 18
MAX_MARKER_SIZE = 3000
fra_pass_between['width'] = (fra_pass_between.counts / fra_pass_between.counts.max() *
                           MAX_LINE_WIDTH)
fra_average_locations['marker_size'] = (fra_average_locations['count']
                                         / fra_average_locations['count'].max() * MAX_MARKER_SIZE)

#Set the color and transparency of lines when fewer passes are made
MIN_TRANSPARENCY = 0
color = np.array(to_rgba('white'))
color = np.tile(color, (len(fra_pass_between), 1))
c_transparency = fra_pass_between.pass_count / fra_pass_between.pass_count.max()
c_transparency = (c_transparency * (1 - MIN_TRANSPARENCY)) + MIN_TRANSPARENCY
color[:, 3] = c_transparency


# Setup the pitch
pitch = Pitch(pitch_type='statsbomb',pitch_color='#3e7d1b', line_color='white', stripe_color='#4c8527', stripe=True)
fig, ax = pitch.draw(figsize=(16, 11), constrained_layout=False, tight_layout=False)


# Creating the passing arrows

# Calculate the adjustment factor for arrow length
ARROW_LENGTH_FACTOR = 0.9  # Adjust this factor to control arrow length

# Creating the passing arrows with adjusted transparency and length
fra_adjusted_end_x = fra_pass_between.starting_x + (fra_pass_between.starting_x_end - fra_pass_between.starting_x) * ARROW_LENGTH_FACTOR
fra_adjusted_end_y = fra_pass_between.starting_y + (fra_pass_between.starting_y_end - fra_pass_between.starting_y) * ARROW_LENGTH_FACTOR

fra_pass_arrows = pitch.arrows(fra_pass_between.starting_x, fra_pass_between.starting_y, 
                               fra_adjusted_end_x, fra_adjusted_end_y, 
                               lw=fra_pass_between.width, color='#FFFFFF', alpha=c_transparency, zorder=1, ax=ax)

#creating the nodes
fra_pass_nodes = pitch.scatter(fra_average_locations.starting_x, fra_average_locations.starting_y, 
                              s=fra_average_locations.marker_size,
                              color='#ED2939', edgecolors='black', linewidth=0.5, alpha=1, ax=ax)
#creating the internal nodes
fra_pass_nodes_interal = pitch.scatter(fra_average_locations.starting_x, fra_average_locations.starting_y,
                              s=fra_average_locations.marker_size / 2, color = '#17548C', edgecolors='black',
                                       linewidth=0.5, alpha=1, ax=ax)

# Add position abbreviations as text labels inside the nodes
for index, row in fra_average_locations.iterrows():
    ax.text(row['starting_x'], row['starting_y'], row.name, color='white',
            fontsize=15, ha='center', va='center', fontweight='bold')

# add title
fig_text(
    0.515, 0.99, "France 4-2-3-1 Passing Map", size=35, fig=fig,
    color='#17548C',
    ha="center", weight="bold"
)

# add subtitle
fig.text(
    0.515, 0.915,
    "2022 FIFA World Cup Final | Post-Match Analysis",
    size=20,
    ha="center", weight="bold", color="#ED2939"
)

# Adding player names and their position played
fra_player_title = "Players"
ax.text(1.15, .95, fra_player_title, fontsize=15, va='center', ha='left', fontweight='bold',
        color="#17548C",transform=ax.transAxes)

# List of France player names
fra_players = [
        'Hugo Lloris(C)',
        'Jules Koundé / Axel Disasi',
        'Raphaël Varane / Ibrahima Konate',
        'Dayot Upamecano',
        'Theo Hernández / Eduardo Camavinga',
        'Aurélien Tchouaméni',
        'Adrien Rabiot / Youssouf Fofana',
        'Ousmane Dembélé / Randal Kolo Muani',
        'Antoine Griezmann / Kingsley Coman',
        'Kylian Mbappé',
        "Olivier Giroud / Marcus Thuram"
]

# Position for the first substitute
x_coordinate = 1.15
y_coordinate = 0.90

# Spacing between player names
line_height = 0.04

# Add the Argentina substitute player names
for players in fra_players:
    ax.text(x_coordinate, y_coordinate, players, fontsize=15, va='center', ha='left', color="#17548C", transform=ax.transAxes)
    y_coordinate -= line_height
    
#Positions
fra_pos_title = "Pos."
ax.text(1.05, .95, fra_pos_title, fontsize=15, va='center', ha='left', fontweight='bold',
        color="#17548C",transform=ax.transAxes)

# List of France Positions
fra_pos = [
    'GK',
    'RB',
    'RCB',
    'LCB',
    'LB',
    'RDM',
    'LDM',
    'RW',
    'CAM',
    'LW',
    "CF",
]

# Position for the first position
pos_x_coordinate = 1.05
pos_y_coordinate = 0.90

# Spacing between player names
pos_line_height = 0.04

# Add the France positions names
for pos in fra_pos:
    ax.text(pos_x_coordinate, pos_y_coordinate, pos, fontsize=15, va='center', ha='left', color="#17548C", transform=ax.transAxes)
    pos_y_coordinate -= pos_line_height
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/France%20Passing%20Map.png)

## 5. Argentina vs France: Shot Map

This graph displays a shot map for both Argentina and France detailing the locations of shots taken throughout the first four periods of regulation in the World Cup Final.


```python
# import matplotlib.pyplot as plt
from matplotlib.patheffects import withStroke

# Setup the pitch
pitch = Pitch(pitch_type='statsbomb', goal_type='box', pitch_color='#3e7d1b', line_color='white', stripe_color='#4c8527', stripe=True)
fig, ax = pitch.draw(figsize=(16, 11), constrained_layout=False, tight_layout=False)

#Plotting Argentina Shots
for x in range(len(argentina_shots['id'])):
    # Let's filter out only shots in regulation (periods 1-4...exclude period 5 penalty shootout)
    if argentina_shots['period'].iloc[x] in [1, 2, 3, 4]:
        # The size of the scatter will be determined by xG
        size = np.sqrt(argentina_shots['shot_statsbomb_xg'].iloc[x]) * 200
        if argentina_shots['shot_outcome_name'].iloc[x] == 'Goal':
            # Plotting goals with a thicker and bolder line
            plt.plot((argentina_shots['location'].iloc[x][0], argentina_shots['shot_end_location'].iloc[x][0]),
                     (argentina_shots['location'].iloc[x][1], argentina_shots['shot_end_location'].iloc[x][1]),
                     color='#D5B048', linewidth=2.5)  # Adjust the linewidth as needed
            pitch.scatter(argentina_shots['location'].iloc[x][0], argentina_shots['location'].iloc[x][1],
                           s=300, marker='football', ax=ax)
        else:
            # Plotting missed shots with a thinner line
            plt.plot((argentina_shots['location'].iloc[x][0], argentina_shots['shot_end_location'].iloc[x][0]),
                     (argentina_shots['location'].iloc[x][1], argentina_shots['shot_end_location'].iloc[x][1]),
                     color='#43A1D5', linewidth=1)  # Adjust the linewidth as needed
            plt.scatter(argentina_shots['location'].iloc[x][0], argentina_shots['location'].iloc[x][1],
                          s=size, color='#43A1D5')

#Plotting France Shots
for x in range(len(france_shots['id'])):
    # Let's filter out only shots in regulation (periods 1-4...exclude period 5 penalty shootout)
    if france_shots['period'].iloc[x] in [1, 2, 3, 4]:
        # The size of the scatter will be determined by xG
        size = np.sqrt(france_shots['shot_statsbomb_xg'].iloc[x]) * 200
        if france_shots['shot_outcome_name'].iloc[x] == 'Goal':
            # Plotting goals with a thicker and bolder line
            plt.plot((120-france_shots['location'].iloc[x][0], 120-france_shots['shot_end_location'].iloc[x][0]),
                     (80-france_shots['location'].iloc[x][1], 80-france_shots['shot_end_location'].iloc[x][1]),
                     color='#ED2939', linewidth=2.5)  # Adjust the linewidth as needed
            pitch.scatter(120-france_shots['location'].iloc[x][0], 80-france_shots['location'].iloc[x][1],
                           s=300, marker='football', ax=ax)
        else:
            # Plotting missed shots with a thinner line
            plt.plot((120-france_shots['location'].iloc[x][0], 120-france_shots['shot_end_location'].iloc[x][0]),
                     (80-france_shots['location'].iloc[x][1], 80-france_shots['shot_end_location'].iloc[x][1]),
                     color='#21304D', linewidth=1)  # Adjust the linewidth as needed
            plt.scatter(120-france_shots['location'].iloc[x][0], 80-france_shots['location'].iloc[x][1],
                          s=size, color='#21304D')   
            
# Let's create the title
title = "Argentina vs France\n2022 FIFA World Cup Final | Shots in Regulation"
ax.set_title(title, fontsize=20, fontweight='bold')

# Add titles and stats to the left half (France)
left_team = "France"
text=ax.text(0.10, 0.90, left_team, fontsize=30, va='center', ha='center', fontweight='bold',
        color="#21304D" ,transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])

fra_total_shots = "Total Shots:"
text=ax.text(0.35, 0.82, fra_total_shots, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])

fra_total_shots2 = "10"
text=ax.text(0.35, 0.78, fra_total_shots2, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#ED2939",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

fra_xG = "Expected Goals"
text=ax.text(0.35, 0.67, fra_xG, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])

fra_xG2 = "(xG): 2.3"
text=ax.text(0.35, 0.63, fra_xG2, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#ED2939",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

fra_goals = "Total Goals:"
text=ax.text(0.35, 0.41, fra_goals, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])

fra_goals2 = "3"
text=ax.text(0.35, 0.37, fra_goals2, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#ED2939",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

fra_pens = "Penalties:"
text=ax.text(0.35, 0.26, fra_pens, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#21304D",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])

fra_pens2 = "2"
text=ax.text(0.35, 0.22, fra_pens2, fontsize=20, va='center', ha='center', fontweight='bold',
        color="#ED2939",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

# Add titles and stats to the right half (Argentina)
right_team = "Argentina"
text=ax.text(0.87, 0.90, right_team, fontsize=28, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_total_shots = "Total Shots:"
text = ax.text(0.65, 0.82, arg_total_shots, fontsize=22, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_total_shots2 = "20"
text = ax.text(0.65, 0.78, arg_total_shots2, fontsize=20, va='center', ha='center', fontweight='bold',
               color="#D5B048", transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_xG = "Expected Goals:"
text=ax.text(0.65, 0.67, arg_xG, fontsize=22, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])
arg_xG2 = "(xG): 2.8"
text=ax.text(0.65, 0.63, arg_xG2, fontsize=20, va='center', ha='center', fontweight='bold', 
        color="#D5B048",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_goals = "Total Goals:"
text=ax.text(0.65, 0.41, arg_goals, fontsize=22, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_goals2 = "3"
text=ax.text(0.65, 0.37, arg_goals2, fontsize=20, va='center', ha='center', fontweight='bold', 
        color="#D5B048",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_pens = "Penalties:"
text=ax.text(0.65, 0.26, arg_pens, fontsize=22, va='center', ha='center', fontweight='bold', 
        color="#43A1D5",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_pens2 = "1"
text=ax.text(0.65, 0.22, arg_pens2, fontsize=20, va='center', ha='center', fontweight='bold', 
        color="#D5B048",transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

fra_GS = "Goalscorers:"
text=ax.text(0.25, 0.12, fra_GS, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#21304D" ,transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=1, foreground='black')])
fra_GS2 = "Kylian Mbappe 80', 82', 118'"
text=ax.text(0.25, 0.08, fra_GS2, fontsize=14, va='center', ha='center', fontweight='bold',
        color="#ED2939" ,transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

arg_GS = "Goalscorers:"
text=ax.text(0.75, 0.12, arg_GS, fontsize=22, va='center', ha='center', fontweight='bold',
        color="#43A1D5" ,transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])
arg_GS2 = "Lionel Messi 23', 108', Angel Di Maria 36'"
text=ax.text(0.75, 0.08, arg_GS2, fontsize=14, va='center', ha='center', fontweight='bold',
        color="#D5B048" ,transform=ax.transAxes)
text.set_path_effects([withStroke(linewidth=3, foreground='black')])

# Show the plot
plt.show()
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/Shot%20Map.png)

## 6. Argentina vs France: Possession Chart

This possession chart visually represents the possession percentages for Argentina and France throughout the full 120 minutes of the match.


```python
# Use Events df and invert possession duration for France (make it negative) so that we can display both teams' possession

for x in range(len(events['index'])):
    if (events['possession_team_id'].iloc[x] == 771):
        events.duration.iloc[x] = events.duration.iloc[x]*(-1)
```
```python
# import matplotlib.pyplot as plt
import numpy as np

# Assuming 'events' is your DataFrame containing data for the chart

# Define custom colors for the bars
arg_color = '#43A1D5'  # light blue
fra_color = '#21304D'  # navy

# Creating the chart with a larger size
fig, ax = plt.subplots(figsize=(10, 6))  # Adjust the width and height as needed
fig.subplots_adjust(top=0.85)

ax.set_xlabel('Minutes')
ax.set_ylabel('Possession')

# Use the specified colors for positive and negative durations
bars = ax.bar(events.minute, events.duration, color=np.where(events.duration > 0, arg_color, fra_color), alpha=0.2)

ax.axhline(0, color='black')
tot_min = events.minute.max()
ax.set_xticks(np.arange(0, tot_min, step=15))

title = "Argentina vs France\n2022 FIFA World Cup Final | Possession Chart"
ax.set_title(title, fontsize=15, fontweight='bold')

# Create legend handles for custom colors
legend_handles = [
    plt.Line2D([0], [0], color=arg_color, lw=4, label='Argentina'),
    plt.Line2D([0], [0], color=fra_color, lw=4, label='France')
]

# Add a legend for the bars with custom colors
legend = ax.legend(handles=legend_handles, loc='upper right', title='Teams', title_fontsize=10, fontsize=8)
```

## ![Image Link](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/Graphs/Possession%20Chart.png)

## [7. Full Code](https://github.com/AustinSaenz/World-Cup-Final-Post-Match-Analysis/blob/main/2022%20FIFA%20World%20Cup%20Final%20Analysis.ipynb)

