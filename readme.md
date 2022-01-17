# UseMyKeypress(hFig, myKeypressFun, customModes)

In certain plot modes (rotate, pan, zoom), MATLAB overwrites keypress
callbacks. This function sets and maintains a custom keypress callback
(with options to ignore/append the custom callback in certain modes).

NOTE:
Uses undocumented features to overwrite MATLAB exploration mode keypress
callbacks with custom keypress function.
See: https://undocumentedmatlab.com/articles/enabling-user-callbacks-during-zoom-pan

Example 1

    % Sets customKey press function
    figure()
    customFun = @(~,evnt) fprintf('Custom keypress function for key %s\n', evnt.Key);
    UseMyKeypress(gcf,customFun)


Example 2

    % This example prints key presses except when in datacursor mode (where
    % left, right keys will move the selected data point).
    % In rotate mode, left, right key presses will both update the plot and
    % also call the custom function (print the pressed key).

    figure()
    customFun = @(~,evnt) fprintf('Custom keypress function for key %s\n', evnt.Key);
    UseMyKeypress(gcf,customFun, ...
        {'Exploration.Datacursor', 'ignore'
        'Exploration.Rotate3d', 'append'});        
    x = linspace(-pi,pi,40);
    plot3(cos(x),sin(x),x);
    view(3)
