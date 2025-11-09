PowerShell Functions and Aliases for Laravel Artisan

This repository (or section) contains PowerShell functions and aliases to make running Laravel Artisan commands faster and more convenient, especially for Windows users. Instead of typing php artisan, you can use a short alias like art or specific functions.

Features
Single Alias: Use a short alias (e.g., art or pa) in place of php artisan.

Argument Support: Passes all arguments and options directly to the underlying php artisan command, including flags (e.g., art make:model Post -mcr).

Easy Setup: Simple function and alias definition you can add to your PowerShell profile.

💻 Installation
To make your alias and function permanent, you need to add them to your PowerShell Profile file, which runs every time you start PowerShell.

Step 1: Check for your Profile File
Open PowerShell and run the following command to see the path to your current profile file:

PowerShell
$profile
If the file does not exist, you can create it with:

PowerShell
New-Item -Path $profile -ItemType File -Force
Step 2: Add the Function and Alias
Open the file path returned by $profile (e.g., using notepad $profile) and add the following PowerShell code:

PowerShell
# Custom function to execute 'php artisan'
function Invoke-ArtisanCommand {
    # The $args automatic variable contains all arguments passed to the function.
    # The '&' operator (call operator) is used to run an external executable.
    & php artisan $args 
}

# Set a short alias for the function
Set-Alias -Name art -Value Invoke-ArtisanCommand
# You may prefer a different alias like 'pa'
# Set-Alias -Name pa -Value Invoke-ArtisanCommand
Step 3: Reload Your Profile
Save the file and either restart your PowerShell terminal or run the following command to reload your profile in the current session:

PowerShell
. $profile
(Note the dot and space before $profile)

Additional Helpful Aliases
You can also create simpler aliases for frequently used composite commands:

PowerShell
# Common development commands
Set-Alias -Name db:migrate -Value "art migrate" -Description "Run database migrations"
Set-Alias -Name db:seed -Value "art db:seed" -Description "Seed the database"
Set-Alias -Name fresh:seed -Value "art migrate:fresh --seed" -Description "Fresh database and seed"
Set-Alias -Name model -Value "art make:model" -Description "Create a new model"
Set-Alias -Name ctrl -Value "art make:controller" -Description "Create a new controller"
Making Aliases Permanent
Remember, to persist these shortcuts across new PowerShell sessions, they must be saved in your $PROFILE file.

To see an older video that explains how to create aliases for Laravel Artisan commands in a terminal environment, check out this guide: Terminal Aliases for Laravel Developers. This video demonstrates how terminal aliases can be used for Laravel developers to save time and increase productivity.
