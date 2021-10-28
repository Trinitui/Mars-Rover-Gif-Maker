# Mars-Rover-Gif-Maker

[Spirit's Navcam](https://i.imgur.com/XwHPEWt.mp4)

https://i.imgur.com/XwHPEWt.mp4


## This script will create a gif from a range of dates (sols) for a given rover.  


    mars_pics = []
    #Change thse parameters
    camera = 'fhaz'
    sol_start = 550 
    sol_end = 600
    rover = 'curiosity'
    verbose_output = 1 # 0 for off, or 1 for on


    for i in range(sol_start,sol_end):
        mars_pics.append(get_images_from_mars_rover_apis(i,API_KEY,camera,verbose_output,rover))
    print("Done with grabbing pics...")
    print("flattening array")

    mars_pics = flatten(mars_pics)

    print("size of Mars Pics list: ",len(mars_pics))
    input("Do you want to continue? Interrupt the Kernel if you don't")

    print("starting image dump to disk (this may take a while...)")
    counter = 0
    for el in mars_pics:
        counter += 1
        urllib.request.urlretrieve(el, f'{counter}.png')
    print("Done with saving...")


    fp_in = r"your_input_dir(where images were saved)*.png"
    fp_out = rf"your_output_dir!\{rover}_gif_{camera}.gif"
    #https://pillow.readthedocs.io/en/stable/handbook/image-file-formats.html#gif


    print("starting gif creation (this may also take a while...)")
    img, *imgs = [Image.open(f) for f in sorted(glob.glob(fp_in))]
    img.save(fp=fp_out, format='GIF', append_images=imgs,
        save_all=True, duration=200, loop=0)

    print('Done!')

